---
title: cross db ownership chaining サーバー構成オプション | Microsoft Docs
description: SQL Server の "cross db ownership chaining" オプションの使用方法について説明します。 複数データベースの組み合わせ所有権をオンまたはオフにする際の考慮事項について説明します。
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 67c453c232d0c448457c1194de898a82ebf46b78
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670635"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining サーバー構成オプション
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **cross db ownership chaining** オプションは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対して、複数データベースの組み合わせ所有権を構成するために使用します。  
  
 このサーバー オプションを使用すると、次に示すように、データベース レベルで複数データベースの組み合わせ所有権を制御したり、すべてのデータベースに複数データベースの組み合わせ所有権を許可できるようになります。  
  
-   インスタンスの **cross db ownership chaining** がオフ (0) になっていると、複数データベースの組み合わせ所有権はすべてのデータベースで無効になります。  
  
-   インスタンスの **cross db ownership chaining** がオン (1) になっていると、複数データベースの組み合わせ所有権はすべてのデータベースで有効になります。  
  
-   ALTER DATABASE ステートメントの SET 句を使用すると、個別のデータベースに複数データベースの組み合わせ所有権を設定できます。 新しいデータベースを作成する場合、CREATE DATABASE ステートメントを使用すると、新しいデータベースに複数データベースの組み合わせ所有権オプションを設定できます。  
  
     **cross db ownership chaining** を 1 に設定することはお勧めしません。この設定を行う場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスによってホストされているすべてのデータベースが複数データベースの組み合わせ所有権に参加する必要があります。また、この設定がセキュリティに与える影響も理解しておく必要があります。  

複数データベースの組み合わせ所有権の現在の状態を確認するには、次のクエリを実行します。  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
結果が 1 の場合は、複数データベースの組み合わせ所有権が有効になっていることを示します。

## <a name="controlling-cross-database-ownership-chaining"></a>複数データベースの組み合わせ所有権の制御  
 複数データベースの組み合わせ所有権のオンとオフを切り替える前に、次の項目について検討する必要があります。  
  
-   複数データベースの組み合わせ所有権のオンとオフを切り替えるには、 **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
-   実稼動サーバーで複数データベースの組み合わせ所有権をオフにするには、サード パーティのアプリケーションを含むすべてのアプリケーションを十分にテストし、この変更がアプリケーションの機能に影響を与えないことを確認します。  
  
-   **sp_configure** で RECONFIGURE を指定すると、サーバーの実行中に **cross db ownership chaining**オプションを変更できます。  
  
-   複数データベースの組み合わせ所有権が必要なデータベースがある場合、推奨される操作としては、まず **sp_configure** を使用してインスタンスの **cross db ownership chaining**オプションをオフにします。次に、ALTER DATABASE ステートメントを使用し、個別のデータベースの複数データベースの組み合わせ所有権をオンにします。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
