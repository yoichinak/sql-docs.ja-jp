---
description: MSSQL_ENG014114
title: MSSQL_ENG014114 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: e98d56ebf3f2439cc36fd0940f8680f3676793c5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198827"
---
# <a name="mssql_eng014114"></a>MSSQL_ENG014114
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|属性|値|  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14114|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|'%s' はディストリビューターとして構成されていません。|  
  
## <a name="explanation"></a>説明  
 エラー メッセージで 'NULL' ではない特定のインスタンスが指定されている場合、指定されたインスタンスはディストリビューターとして認識されるように正しく構成されていません。  
  
 メッセージで 'NULL' がディストリビューターとして指定されている場合、 **master** データベースのローカル サーバーにエントリがないか、エントリが正しくありません (おそらくコンピューターの名前が変更されたことが原因です)。 レプリケーションでは、コンピューター名とオプションのインスタンス名 (クラスター化されたインスタンスの場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仮想サーバー名とオプションのインスタンス名) を使用して、トポロジのすべてのサーバーを登録する必要があります。 レプリケーションが正しく機能するためには、トポロジの各サーバーに対して `SELECT @@SERVERNAME` によって返された値が、コンピューター名または仮想サーバー名と、オプションのインスタンス名で一致している必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのいずれかを IP アドレスまたは完全修飾ドメイン名 (FQDN) で登録している場合、レプリケーションはサポートされません。 レプリケーションの構成時に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内に IP アドレスまたは FQDN で登録された [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] インスタンスがあった場合、このエラーが発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 エラー メッセージで特定のインスタンスが指定されている場合、サーバーをディストリビューターとして構成してください。 詳しくは、「 [Configure Distribution](../../relational-databases/replication/configure-distribution.md)」を参照してください。  
  
 エラー メッセージで特定のインスタンスが指定されていない (つまり 'NULL' である) 場合、ディストリビューター インスタンスが正しく登録されていることを確認してください。 コンピューターのネットワーク名と SQL Server インスタンスの名前が異なる場合は、次のいずれかを実行してください。  
  
-   SQL Server インスタンス名を有効なネットワーク名として追加します。 代替ネットワーク名を設定する 1 つの方法は、その名前をローカル ホスト ファイルに追加することです。 ローカル ホスト ファイルは、既定では、WINDOWS\system32\drivers\etc または WINNT\system32\drivers\etc にあります。詳細については、Windows のマニュアルを参照してください。  
  
     たとえば、コンピューター名が comp1、そのコンピューターの IP アドレスが 10.193.17.129、インスタンス名が inst1/instname の場合、ホスト ファイルに次のエントリを追加します。  
  
     10.193.17.129 inst1  
  
-   ディストリビューションを無効化し、インスタンスを登録して、ディストリビューションを再設定してください。 @@SERVERNAME の値が、クラスター化されていないインスタンスに対して適切でない場合は、次の手順を実行してください。  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) ストアド プロシージャを実行したら、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動し、@@SERVERNAME への変更を有効にする必要があります。  
  
     @@SERVERNAME の値がクラスター化されたインスタンスに対して適切でない場合は、クラスター アドミニストレーターを使用して名前を変更する必要があります。 詳細については、「[Always On フェールオーバー クラスター インスタンス (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
