---
title: データベース マスター キーのバックアップ | Microsoft Docs
description: Transact-SQL を使用して SQL Server でデータベース マスター キーをバックアップする方法について説明します。 この重要なキーにより、他のキーと証明書が暗号化されます。
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], exporting
ms.assetid: 7ad9a0a0-6e4f-4f7b-8801-8c1b9d49c4d8
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 92e8753033e37561b23f2e1d15cb06cef4b662d7
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250687"
---
# <a name="back-up-a-database-master-key"></a>データベース マスター キーのバックアップ
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用してデータベース マスター キーをバックアップする方法について説明します。 データベース マスター キーは、データベース内の他のキーや証明書を暗号化する際に使用します。 データベース マスター キーが削除されるか破損すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、暗号化されたキーの暗号化を解除できなくなる場合があります。さらに、そのキーを使用して暗号化されたデータは事実上失われます。 このため、データベース マスター キーはバックアップして、安全な別の場所に保存しておく必要があります。  
  
## <a name="before-you-begin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
  
- マスター キーは開かれている必要があります。したがって、バックアップ前に暗号化を解除する必要があります。 マスター キーがサービス マスター キーで暗号化されている場合は、明示的に開く必要はありません。 パスワードのみで暗号化されている場合は、明示的に開く必要があります。  
  
- マスター キーは作成後すぐにバックアップし、安全な別の場所に保存することをお勧めします。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可
データベースに対する CONTROL 権限が必要です。  
  
## <a name="using-sql-server-management-studio-with-transact-sql"></a>Transact-SQL を備えた SQL Server Management Studio の使用  
  
### <a name="to-back-up-the-database-master-key"></a>データベース マスター キーをバックアップするには  
  
1. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、バックアップするデータベース マスター キーが格納されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
2. バックアップ メディアでデータベース マスター キーの暗号化に使用するパスワードを指定します。 このパスワードに対しては、複雑性がチェックされます。  
  
3. バックアップしたキーのコピーを保存するためにリムーバブル バックアップ メディアを用意します。  
  
4. キーのバックアップを作成する NTFS ディレクトリを指定します。 このディレクトリは、次の手順で指定するファイルの作成先となります。 このディレクトリは、制限の厳しいアクセス制御リスト (ACL) で保護する必要があります。  
  
5. **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
6. [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
7. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql
    -- Creates a backup of the "AdventureWorks2012" master key. Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;   
    GO  
    OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';   
  
    BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
        ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';   
    GO  
    ```  
  
    > [!NOTE]  
    > キーのファイル パスとキーのパスワード (存在する場合) は、実際は上に示したものと異なります。 両方がサーバーとキーのセットアップで固有であることをご確認ください。  
  
8. ファイルをバックアップ メディアにコピーして、コピーしたファイルを確認します。  
  
9. バックアップを安全な場所に保存します。  
  
 詳細については、「[OPEN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-master-key-transact-sql.md)」と「[BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-master-key-transact-sql.md)」を参照してください。  
