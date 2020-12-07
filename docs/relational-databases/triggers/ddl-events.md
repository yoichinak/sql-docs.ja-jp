---
description: DDL イベント
title: DDL イベント | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25cdef293ced7b58ea41f71f78a1046c6b5dd0ba
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128633"
---
# <a name="ddl-events"></a>DDL イベント
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  次の表は、DDL トリガーまたはイベント通知を起動するために使用できる DDL イベントの一覧です。 各イベントは、キーワード間にアンダースコア文字 (_) を含めるように変更されたステートメント構文を備えた [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたはストアド プロシージャに対応しています。  
  
> [!IMPORTANT]  
>  DDL と同様の操作を実行するシステム ストアド プロシージャも、DDL トリガーとイベント通知を起動します。 実行されるシステム ストアド プロシージャへの応答を判断するために、DDL トリガーおよびイベント通知をテストしてください。 たとえば、CREATE TYPE ステートメントおよび **sp_addtype** ストアド プロシージャはどちらも、CREATE_TYPE イベントで作成される DDL トリガーおよびイベント通知を起動します。  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>サーバー スコープまたはデータベース スコープを持つ DDL ステートメント  
 DDL トリガーまたはイベント通知は、そのトリガーまたはイベント通知が作成されたデータベース、またはサーバー インスタンスのあらゆる場所で、次に示すイベントが発生したときにそのイベントに応答して起動されるように作成できます。  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE (CREATE APPLICATION ROLE ステートメントと **sp_addapprole** に適用されます。 新しいスキーマが作成されると、このイベントは CREATE_SCHEMA イベントもトリガーします。)
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE (ALTER APPLICATION ROLE ステートメントと **sp_approlepassword** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE (DROP APPLICATION ROLE ステートメントと **sp_dropapprole** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE (ON DATABASE が指定されている場合の ALTER AUTHORIZATION ステートメント、および **sp_changedbowner** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT ( **sp_bindefault** に適用されます。)
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT ( **sp_unbindefault** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY ( **sp_addextendedproperty** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY ( **sp_updateextendedproperty** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY ( **sp_dropextendedproperty** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG (CREATE FULLTEXT CATALOG ステートメントと、 **create** が指定されている場合の *sp_fulltextcatalog* に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG (ALTER FULLTEXT CATALOG ステートメント、 **start_incremental** 、 *start_full*、 *Stop*、または *Rebuild* が指定されている場合の *sp_fulltextcatalog* 、および **enable** が指定されている場合の *sp_fulltext_database* に適用されます。)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG (DROP FULLTEXT CATALOG ステートメントと、 **drop** が指定されている場合の *sp_fulltextcatalog* に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX (CREATE FULLTEXT INDEX ステートメントと、 **create** が指定されている場合の *sp_fulltexttable* に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX (ALTER FULLTEXT INDEX ステートメント、 **start_full** 、 *start_incremental*、または *stop* が指定されている場合の *sp_fulltextcatalog* 、 **sp_fulltext_column**、および **create** または *drop* 以外のアクションが指定されている場合の *sp_fulltext_table* に適用されます。)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX (DROP FULLTEXT INDEX ステートメントと、 **drop** が指定されている場合の *sp_fulltexttable* に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX (ALTER INDEX ステートメントと **sp_indexoption** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE ( **sp_create_plan_guide** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE (ENABLE、ENABLE ALL、DISABLE、または DISABLE ALL が指定されている場合の **sp_control_plan_guide** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE (DROP または DROP ALL が指定されている場合の **sp_control_plan_guide** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE (ALTER PROCEDURE ステートメントと **sp_procoption** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME ( **sp_rename** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE (CREATE ROLE ステートメント、 **sp_addrole**、および **sp_addgroup** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE (DROP ROLE ステートメント、 **sp_droprole**、および **sp_dropgroup** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE ( **sp_bindrule** に適用されます。)
    :::column-end:::
    :::column:::
        UNBIND_RULE ( **sp_unbindrule** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA (CREATE SCHEMA ステートメント、 **sp_addrole**、 **sp_adduser**、 **sp_addgroup**、および **sp_grantdbaccess** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_SCHEMA (ALTER SCHEMA ステートメントと **sp_changeobjectowner** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE (非スキーマ スコープ オブジェクト (データベース、アセンブリ、トリガー) の署名操作用)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT (スキーマ スコープ オブジェクト (ストアド プロシージャ、関数) 用)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX は、空間インデックスに使用できます。
    :::column-end:::
    :::column:::
        DROP_INDEX は、空間インデックスに使用できます。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE (ALTER TABLE ステートメントと **sp_tableoption** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER (ALTER TRIGGER ステートメントと **sp_settriggerorder** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE (CREATE TYPE ステートメントと **sp_addtype** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_TYPE (DROP TYPE ステートメントと **sp_droptype** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER (CREATE USER ステートメント、 **sp_adduser**、および **sp_grantdbaccess** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_USER (ALTER USER ステートメントと **sp_change_users_login** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_USER (DROP USER ステートメント、 **sp_dropuser**、および **sp_revokedbaccess** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX は、XML インデックスに使用できます。
    :::column-end:::
    :::column:::
        DROP_INDEX は、XML インデックスに使用できます。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>サーバー スコープを持つ DDL ステートメント  
 DDL トリガーまたはイベント通知は、サーバー インスタンスのあらゆる場所で次に示すイベントが発生したときに、そのイベントに応答して起動されるように作成できます。  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE (ローカル サーバー インスタンスが指定されている場合の **sp_configure** と **sp_addserver** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE (ALTER DATABASE ステートメントと **sp_fulltext_database** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE ( **sp_addextendedproc** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE ( **sp_dropextendedproc** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER ( **sp_addlinkedserver** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER ( **sp_serveroption** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER (リンク サーバーが指定されている場合の **sp_dropserver** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN ( **sp_addlinkedsrvlogin** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN ( **sp_droplinkedsrvlogin** に適用されます。)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN (暗黙的に作成する必要がある存在しないログインで使用される場合の CREATE_LOGIN ステートメント、 **sp_addlogin**、 **sp_grantlogin**、 **xp_grantlogin**、および **sp_denylogin** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_LOGIN ( **Auto_Fix** が指定されている場合の ALTER LOGIN ステートメント、 **sp_defaultdb**、 **sp_defaultlanguage**、 **sp_password** 、および *sp_change_users_login* に適用されます。)
    :::column-end:::
    :::column:::
        DROP_LOGIN (DROP LOGIN ステートメント、 **sp_droplogin**、 **sp_revokelogin**、および **xp_revokelogin** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE ( **sp_addmessage** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_MESSAGE ( **sp_altermessage** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_MESSAGE ( **sp_dropmessage** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER ( **sp_addserver** に適用されます。)
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER ( **sp_setnetname** に適用されます。)
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER (リモート サーバーが指定されている場合の **sp_dropserver** に適用されます。)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>参照  
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)   
 [イベント通知](../../relational-databases/service-broker/event-notifications.md)   
 [DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
