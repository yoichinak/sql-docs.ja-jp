---
title: メモリ最適化テーブルのストレージの構成 | Microsoft Docs
description: SQL Server で、メモリ最適化テーブルのストレージ容量と 1 秒あたりの入出力操作 (IOPS) を構成する方法について説明します。
ms.custom: ''
ms.date: 1/15/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a88af1af1e814ee6340f72553d74fdba1247c51e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542905"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>メモリ最適化テーブルのストレージの構成
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  記憶域の容量と 1 秒間の入出力操作 (IOPS) を構成する必要があります。  
  
## <a name="storage-capacity"></a>ストレージの容量  

[メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) の情報を使用して、データベースの持続性のあるメモリ最適化テーブルのメモリ内サイズを推定します。 インデックスはメモリ最適化テーブルに対して永続化されないため、インデックスのサイズは含めません。 
 
サイズを決定した後、新しく変更されたデータを格納するために使用される、チェックポイント ファイルを保持するのに十分なディスク領域を提供する必要があります。 格納されるデータには、インメモリ テーブルに追加された新しい行の内容だけでなく、既存の行の新しいバージョンも含まれます。 この記憶域は、行が挿入または更新されると大きくなります。 ログの切り捨てが発生すると、行バージョンはマージされ、記憶域は回収されます。 何らかの理由でログの切り捨てが遅れると、インメモリ OLTP ストアが大きくなります。

この領域のストレージのサイズを設定する場合、最初は、持続性のあるインメモリ テーブルのサイズの 4 倍を予約することをお勧めします。 領域の使用量を監視し、必要に応じて使用可能な記憶域を拡張できるように準備します。
  
## <a name="storage-iops"></a>記憶域の IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] は、ワークロードのスループットを大幅に上げることができます。 したがって、IO がボトルネックになっていないことを確認してください。  
  
-   ディスク ベース テーブルをメモリ最適化テーブルに移行するときは、トランザクション ログ アクティビティの増加をサポートできる記憶メディアにトランザクション ログがあることを確認してください。 たとえば、記憶メディアが 100 MB/秒のトランザクション ログの処理をサポートし、その結果としてメモリ最適化テーブルが 5 倍優れたパフォーマンスをもたらす場合、トランザクション ログ アクティビティがパフォーマンスのボトルネックになることを防ぐために、トランザクション ログの記憶メディアでも、5 倍のパフォーマンス向上をサポートできる必要があります。  
  
-   メモリ最適化テーブルは、1 つまたは複数のコンテナーに分散されたチェックポイント ファイルに保存されます。 各コンテナーは、通常、独自のストレージ デバイスにマップする必要があり、増加する記憶域容量と IOPS の向上の両方のために使用されます。 ストレージ メディアのシーケンシャル IOPS が、持続的トランザクション ログ スループットの最大 3 倍をサポートできることを確認する必要があります。 チェックポイント ファイルへの書き込みは、データ ファイルの場合は 256 KB、差分ファイルの場合は 4 KB です。
  
     - たとえば、メモリ最適化テーブルがトランザクション ログで持続的に 500 MB/秒のアクティビティを生成する場合、メモリ最適化テーブルのストレージは 1.5 GB/秒の IOPS をサポートする必要があります。 持続的なトランザクション ログのスループットの 3 倍をサポートする必要性は、次の観察点に由来します。すなわち、データとデルタ ファイルのペアは、まず初期データと共に書き込まれ、それからマージ操作の一環として読み取り/再書き込みされる必要があるという点です。  
  
- 記憶域の IOPS を見積もる際のもう 1 つの要因は、メモリ最適化テーブルの復旧時間です。 持続性のあるテーブルからのデータは、データベースがアプリケーションで使用される前にメモリに読み込む必要があります。 一般的に、メモリ最適化テーブルへのデータの読み込みは IOPS の速度で実行できます。 それで、持続性のあるメモリ最適化テーブルの合計の記憶域が 60 GB で、1 分でこのデータを読み込めるようにする場合は、記憶域の IOPS を 1 GB/秒に設定する必要があります。  
  
-   スペースが許す場合は、通常、チェックポイント ファイルはすべてのコンテナーに均等に分散されます。 SQL server 2014 では、均一な分散を実現するには奇数個のコンテナーが必要です。2016 以降では、コンテナーが奇数または偶数のどちらでも、均一に分散されます。
  
## <a name="encryption"></a>暗号化  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降のバージョンでは、データベース上で Transparent Data Encryption (TDE) を有効にする際に、メモリ最適化テーブルのストレージは保存時に暗号化されます。 詳細については、「[透過的なデータ暗号化](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] では、データベースで TDE が有効になっている場合でも、チェックポイント ファイルは暗号化されません。

 [持続性のない](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md) (SCHEMA_ONLY) メモリ最適化テーブルのデータは、常にディスクに書き込まれません。 そのため、TDE は、このようなテーブルには適用されません。
  
## <a name="see-also"></a>参照  
 [メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
