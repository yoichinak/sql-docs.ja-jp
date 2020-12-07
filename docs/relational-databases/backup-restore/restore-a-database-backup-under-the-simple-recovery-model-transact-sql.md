---
title: データベースの復元 - 単純復旧モデル (Transact-SQL)
description: この記事では、Transact-SQL を使用して、単純復旧モデルで SQL Server データベースの完全バックアップを復元する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
author: cawrites
ms.author: chadam
ms.openlocfilehash: 508e567be5fa44e3bf64465dc583f7196dcdb911
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129131"
---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>単純復旧モデルでのデータベース バックアップの復元 (Transact-SQL)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、データベースの完全バックアップを復元する方法について説明します。  
  
> [!IMPORTANT]  
>  データベースの完全バックアップの復元中は、復元作業を実行するシステム管理者以外は、復元中のデータベースを使用しないでください。  
  
## <a name="prerequisites-and-recommendations"></a>前提条件と推奨事項  
  
-   暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
-   セキュリティを確保するため、不明なソースや信頼されていないソースからのデータベースは、アタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
## <a name="database-compatibility-level-after-upgrade"></a>アップグレード後のデータベース互換性レベル  
 **tempdb**、 **model**、 **msdb** 、および **Resource** データベースの互換性レベルは、アップグレード後に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の互換性レベルに設定されます。 **master** システム データベースは、互換性レベルが 100 を下回っている場合を除いて、アップグレード前の互換性レベルを保持します。 アップグレード前の **master** の互換性レベルが 100 を下回っている場合は、アップグレード後、100 に設定されます。  
  
 アップグレード前のユーザー データベースの互換性レベルが 100 以上の場合は、アップグレード後も互換性レベルは変わりません。 アップグレード前の互換性レベルが 90 の場合、アップグレードされたデータベースの互換性レベルは 100 に設定されます。これは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でサポートされている下限の互換性レベルです。  
  
> [!NOTE]  
>  新しいユーザー データベースには、 **model** データベースの互換性レベルが継承されます。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-restore-a-full-database-backup"></a>データベースの完全バックアップを復元するには  
  
1.  次の項目を指定した RESTORE DATABASE ステートメントを実行し、データベースの完全バックアップを復元します。  
  
    -   復元するデータベースの名前。  
  
    -   データベースの完全バックアップの復元元バックアップ デバイス。  
  
    -   NORECOVERY 句。データベースの完全バックアップを復元した後に適用するトランザクション ログまたはデータベースの差分バックアップがある場合に指定します。  
  
    > [!IMPORTANT]  
    >  暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
2.  必要に応じて、以下も指定します。  
  
    -   FILE 句。バックアップ デバイス上の復元するバックアップ セットを識別するとき指定します。  
  
> [!NOTE]  
>  以前のバージョンのデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に復元すると、データベースが自動的にアップグレードされます。 通常、データベースは直ちに使用可能になります。 ただし、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースにフルテキスト インデックスがある場合、アップグレード プロセスでは、  **upgrade_option** サーバー プロパティの設定に応じて、インポート、リセット、または再構築が行われます。 アップグレード オプションがインポート (**upgrade_option** = 2) または再構築 (**upgrade_option** = 0) に設定されている場合、アップグレード中はフルテキスト インデックスを使用できなくなります。 インデックスを作成するデータ量によって、インポートには数時間、再構築には最大でその 10 倍の時間がかかることがあります。 また、アップグレード オプションがインポートに設定されており、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 **upgrade_option** サーバー プロパティの設定を変更するには、 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)を使用します。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 この例では、テープから [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] の完全データベース バックアップを復元します。  
  
### <a name="example"></a>例  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベースの全体復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [データベースの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)  
  
  
