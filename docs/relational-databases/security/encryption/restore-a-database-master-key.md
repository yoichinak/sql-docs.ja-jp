---
title: データベース マスター キーの復元 | Microsoft Docs
description: SQL Server Management Studio と Transact-SQL を使用して SQL Server でデータベース マスター キーを復元する方法について説明します。
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 65441ecd309abbe9b1545de622f0f7d9d4c2d4bc
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250519"
---
# <a name="restore-a-database-master-key"></a>データベース マスター キーの復元
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[tsql](../../../includes/tsql-md.md)]でデータベース マスター キーを復元する方法について説明します。  
  
## <a name="before-you-begin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
  
- マスター キーを復元するとき、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では現在アクティブなマスター キーによって暗号化されたすべてのキーの暗号化が解除された後、復元されたマスター キーを使用してこれらのキーが暗号化されます。 この操作はリソースを大量に消費するため、リソース要求が少ないときに実行するように考慮してください。 現在のデータベースのマスター キーが開いていないか、開けない場合、またはマスター キーで暗号化されたキーを 1 つでも暗号化解除できない場合、復元操作は失敗します。  
  
- 暗号化解除が 1 つでも失敗した場合、復元は失敗します。 FORCE オプションを使用するとエラーを無視できますが、暗号化を解除できないデータが失われる可能性があります。  
  
- マスター キーがサービス マスター キーで暗号化されている場合は、復元されたマスター キーもサービス マスター キーで暗号化されます。  
  
- 現在のデータベースにマスター キーが存在しない場合は、RESTORE MASTER KEY を実行するとマスター キーが作成されます。 この新しいマスター キーは、サービス マスター キーで自動的に暗号化されません。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可
データベースに対する CONTROL 権限が必要です。  
  
## <a name="using-sql-server-management-studio-with-transact-sql"></a>Transact-SQL を備えた SQL Server Management Studio の使用  
  
### <a name="to-restore-the-database-master-key"></a>データベース マスター キーを復元するには  
  
1. バックアップしたデータベース マスター キーのコピーを、物理バックアップ メディアまたはローカル ファイル システム上のディレクトリから取得します。  
  
2. **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
3. [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
4. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  

    ```sql
    -- Restores the database master key of the AdventureWorks2012 database.  
    USE AdventureWorks2012;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    > キーのファイル パスとキーのパスワード (存在する場合) は、実際は上に示したものと異なります。 両方がサーバーとキーのセットアップで固有であることをご確認ください。  
  
 詳細については、「[RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)」を参照してください。  
