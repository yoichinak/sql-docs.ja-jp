---
description: トリガーのセキュリティの管理
title: トリガーのセキュリティの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 73e56eb0ffcc4996ddd6903f2e79c14947b9a450
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485393"
---
# <a name="manage-trigger-security"></a>トリガーのセキュリティの管理

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

既定では、DML トリガーも DDL トリガーも、トリガーを呼び出したユーザーのコンテキストで実行されます。 トリガーの呼び出し元は、トリガーが実行される原因となったステートメントを実行したユーザーです。 たとえば、ユーザー **Mary** が DELETE ステートメントを実行し、このために DML トリガー **DML_trigMary** が実行された場合、 **DML_trigMary** 内のコードは、 **Mary**のユーザー権限のコンテキストで実行されます。 この既定の動作は、悪意のあるコードをデータベースやサーバー インスタンスに組み込もうとするユーザーによって悪用される危険性があります。 たとえば、次の DDL トリガーがユーザー **JohnDoe** により作成されたとします。  

```sql
CREATE TRIGGER DDL_trigJohnDoe
ON DATABASE
FOR ALTER_TABLE
AS
SET NOCOUNT ON;

BEGIN TRY
  EXEC(N'
    USE [master];
    GRANT CONTROL SERVER TO [JohnDoe];
');
END TRY
BEGIN CATCH
  DECLARE @DoNothing INT;
END CATCH;
GO
```

このトリガーの内容は、`GRANT CONTROL SERVER` sysadmin **固定サーバー ロールのメンバーなど、** ステートメントを実行する権限を持ったユーザーが `ALTER TABLE` ステートメントを実行した直後に、**JohnDoe** に `CONTROL SERVER` 権限を付与するようにしています。 つまり、**JohnDoe** 自身は `CONTROL SERVER` 権限を自分に付与することはできませんが、トリガー コードを利用して、上位の特権の下での実行権限を獲得しています。 DML トリガーも DDL トリガーも、このようなセキュリティの脅威にさらされています。  
  
## <a name="trigger-security-best-practices"></a>トリガーのセキュリティに関するベスト プラクティス  
 次の方法を使用することで、トリガー コードが上位の特権の下で実行されないようにすることができます。  
  
::: moniker range=">=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current"

-   [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) カタログ ビューと [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) カタログ ビューをクエリし、データベースとサーバー インスタンスに存在する DML トリガーおよび DDL トリガーを認識します。 次のクエリは、現在のデータベースにあるすべての DML とデータベースレベルのすべての DDL トリガーと、サーバー インスタンスにあるすべてのサーバー レベルの DDL トリガーを返します。  
  
    ```sql
    SELECT type, name, parent_class_desc FROM sys.triggers
    UNION ALL
    SELECT type, name, parent_class_desc FROM sys.server_triggers;
    ```  

   > [!NOTE]
   > [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)] を使用している場合を除き、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で使用できるのは **sys.triggers** のみです。

::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

-   [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) カタログ ビューに対してクエリを実行して、データベースに存在する DML および DDL トリガーを認識します。 次のクエリでは、現在のデータベースにあるすべての DML とデータベースレベルの DDL トリガーが返されます。  
  
    ```sql
    SELECT type, name, parent_class_desc FROM sys.triggers;
    ```  
  
::: moniker-end

-   [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) を使用して、トリガーが上位の特権の下で実行された場合に、データベースやサーバーの整合性に支障をきたす可能性のあるトリガーを無効にします。 次のステートメントは、現在のデータベースにあるすべてのデータベースレベルの DDL トリガーを無効にします。  
  
    ```sql
    DISABLE TRIGGER ALL ON DATABASE;
    ```  
  
     このステートメントは、サーバー インスタンスにあるすべてのサーバーレベルの DDL トリガーを無効にします。  
  
    ```sql
    DISABLE TRIGGER ALL ON ALL SERVER;
    ```  
  
     このステートメントは、現在のデータベースにあるすべての DML トリガーを無効にします。  
  
    ```sql
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname;
    DECLARE @sql nvarchar(max);
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR
        SELECT SCHEMA_NAME(schema_id) AS schema_name,
            name AS trigger_name,
            OBJECT_NAME(parent_object_id) AS object_name
        FROM sys.objects WHERE type IN ('TR', 'TA');

    OPEN trig_cur;
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name;
  
    WHILE @@FETCH_STATUS = 0
    BEGIN
        SELECT @sql = N'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + N'.'
            + QUOTENAME(@trigger_name)
            + N' ON ' + QUOTENAME(@schema_name) + N'.'
            + QUOTENAME(@object_name) + N'; ';
        EXEC (@sql);
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name;
    END;
    GO

    -- Verify triggers are disabled. Should return an empty result set.
    SELECT * FROM sys.triggers WHERE is_disabled = 0;
    GO

    CLOSE trig_cur;
    DEALLOCATE trig_cur;
    ```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DML トリガー](../../relational-databases/triggers/dml-triggers.md)   
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)  
 [ログオン トリガー](../../relational-databases/triggers/logon-triggers.md)  
  
