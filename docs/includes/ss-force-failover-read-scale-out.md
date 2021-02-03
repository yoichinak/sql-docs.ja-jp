---
title: SQL Server が可用性グループを強制的にフェールオーバーする
description: クラスターの種類が NONE の可用性グループの強制フェールオーバーを実行する
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: fa97b4a86fd4275b12f784ce40d6d03139e3d52e
ms.sourcegitcommit: f30b5f61c514437ea58acc5769359c33255b85b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2021
ms.locfileid: "99214461"
---
各可用性グループにはプライマリ レプリカが 1 つだけあります。 プライマリ レプリカは読み書きができます。 プライマリになっているレプリカの変更は、フェールオーバーで行うことができます。 一般的な可用性グループでは、クラスター マネージャーによってフェールオーバー プロセスが自動化されます。 クラスターの種類が NONE の可用性グループでは、フェールオーバー プロセスは手動です。

クラスターの種類が NONE の可用性グループでプライマリ レプリカをフェールオーバーするには、2 つの方法があります。

- データ損失のない手動フェールオーバー
- データ損失のある強制的な手動フェールオーバー


### <a name="manual-failover-without-data-loss"></a>データ損失のない手動フェールオーバー

プライマリ レプリカを使用できても、プライマリ レプリカをホストするインスタンスを一時的または永続的に変更する必要がある場合は、この方法を使用します。
データ損失の可能性を排除するため、手動フェールオーバーを実行する前にターゲット セカンダリ レプリカが最新の状態であることを確認します。

データ損失のない手動フェールオーバーを行うには:

1. 現在のプライマリおよびターゲット セカンダリ レプリカを `SYNCHRONOUS_COMMIT` とします。

   ```SQL
   ALTER AVAILABILITY GROUP [AGRScale] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

1. アクティブなトランザクションが、プライマリ レプリカと少なくとも 1 つの同期セカンダリ レプリカにコミットされていることを確認するために、次のクエリを実行します。

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   `synchronization_state_desc` が `SYNCHRONIZED` の場合、セカンダリ レプリカは同期されています。

1. `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` を 1 に更新します。

   次の例のスクリプトは、`ag1` という名前の可用性グループで `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` を 1 に設定します。 次のスクリプトを実行する前に、`ag1` を実際の可用性グループの名前に置き換えます。

   ```SQL
   ALTER AVAILABILITY GROUP [AGRScale] 
        SET (REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1);
   ```

   この設定により、すべてのアクティブなトランザクションが、プライマリ レプリカと少なくとも 1 つの同期セカンダリ レプリカにコミットされます。
   >[!NOTE]
   >この設定は、フェールオーバーに固有のものではなく、環境の要件に基づいて設定する必要があります。

1. プライマリ レプリカをオフラインに設定して、ロールの変更に備えます。 

   ```SQL
   ALTER AVAILABILITY GROUP [AGRScale] OFFLINE
   ```

1. ターゲット セカンダリ レプリカをプライマリに昇格させます。

   ```SQL
   ALTER AVAILABILITY GROUP AGRScale FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```

1. 以前のプライマリのロールを `SECONDARY` に更新し、以前のプライマリ レプリカをホストする SQL Server インスタンスで次のコマンドを実行します。

   ```SQL
   ALTER AVAILABILITY GROUP [AGRScale] 
        SET (ROLE = SECONDARY); 
   ```

   > [!NOTE]
   > 可用性グループを削除するには、[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md) を使います。 種類が NONE または EXTERNAL のクラスターを使って作成された可用性グループでは、可用性グループに含まれるすべてのレプリカでコマンドを実行する必要があります。

1. データ移動を再開し、プライマリ レプリカがホストされている SQL Server インスタンス上の可用性グループ内のすべてのデータベースに対して、次のコマンドを実行します。

   ```SQL
   ALTER DATABASE [db1]
        SET HADR RESUME
   ```

1. 読み取りスケールの目的で作成した、クラスター マネージャーでは管理されないリスナーをすべて再作成します。 元のリスナーが以前のプライマリを指している場合、それを削除して、新しいプライマリを指すように再作成します。

### <a name="forced-manual-failover-with-data-loss"></a>データ損失のある強制的な手動フェールオーバー

プライマリ レプリカが利用できず、復旧をすぐに行えない場合は、データ損失を伴うセカンダリ レプリカへのフェールオーバーを強制的に実行する必要があります。 ただし、フェールオーバー後に元のプライマリ レプリカが回復した場合は、それによってプライマリの役割が引き継がれます。 各レプリカが異なる状態になるのを回避するには、データ損失を伴う強制フェールオーバー後に、可用性グループから元のプライマリを削除します。 元のプライマリがオンラインに戻ったら、その中の可用性グループ全体を削除します。 

プライマリ レプリカ N1 からセカンダリ レプリカ N2 へのデータ損失を伴う手動フェールオーバーを強制的に実行するには、次の手順を行います。 

1. セカンダリ レプリカ (N2) で、強制フェールオーバーを開始します。 

    ```SQL
    ALTER AVAILABILITY GROUP [AGRScale] FORCE_FAILOVER_ALLOW_DATA_LOSS;
    ```
    
1. 新しいプライマリ レプリカ (N2) 上で、元のプライマリ (N1) を削除します。 

    ```SQL
    ALTER AVAILABILITY GROUP [AGRScale]
    REMOVE REPLICA ON N'N1';
    ```
    
1. すべてのアプリケーション トラフィックがリスナーまたは新しいプライマリ レプリカに向けられていることを確認します。 
1. 元のプライマリ (N1) がオンラインになった場合は、直ちに、元のプライマリ (N1) 上で可用性グループ AGRScale をオフラインにします。

   ```SQL
   ALTER AVAILABILITY GROUP [AGRScale] OFFLINE
   ```
1. データまたは同期されていない変更がある場合は、ビジネス ニーズに合わせてバックアップまたはその他のデータ レプリケート オプションを使用して、そのデータを保存します。     
1. 次に、元のプライマリ (N1) から可用性グループを削除します。

    ```SQL
    DROP AVAILABILITY GROUP [AGRScale];
    ```
1. 元のプライマリ レプリカ (N1) 上の可用性グループ データベースを削除します。 

    ```SQL
    USE [master]
    GO
    DROP DATABASE [AGDBRScale]
    GO
    ```
    
 1. (省略可能) 必要に応じて、N1 を新しいセカンダリ レプリカとして可用性グループ AGRScale に追加できるようになりました。
