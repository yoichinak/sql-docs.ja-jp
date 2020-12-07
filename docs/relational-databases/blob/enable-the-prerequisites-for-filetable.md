---
title: FileTable の前提条件の有効化 | Microsoft Docs
description: Filetable を使用するには、まず FILESTREAM を有効にし、ディレクトリを指定して、特定のオプションとアクセス レベルを設定します。 すべての前提条件を満たす方法について学習します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 12e392d083b9b47e3330d8a95b6c2d199a146cea
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809923"
---
# <a name="enable-the-prerequisites-for-filetable"></a>FileTable の前提条件の有効化
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  FileTable を作成および使用するための前提条件を有効にする方法について説明します。  
  
##  <a name="enabling-the-prerequisites-for-filetable"></a><a name="EnablePrereq"></a> FileTable の前提条件の有効化  
 FileTable を作成および使用するための前提条件を有効にするには、次の項目を有効にします。  
  
-   **インスタンス レベル:**  
  
    -   [インスタンス レベルでの FILESTREAM の有効化](#BasicsFilestream)  
  
-   **データベース レベル:**  
  
    -   [データベース レベルでの FILESTREAM ファイル グループの指定](#filegroup)  
  
    -   [データベース レベルでの非トランザクション アクセスの有効化](#BasicsNTAccess)  
  
    -   [データベース レベルでの FileTable のディレクトリ指定](#BasicsDirectory)  
  
##  <a name="enabling-filestream-at-the-instance-level"></a><a name="BasicsFilestream"></a> インスタンス レベルでの FILESTREAM の有効化  
 FileTable は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の FILESTREAM 機能を拡張します。 したがって、FileTable を作成および使用するには、ファイル I/O アクセス用の FILESTREAM を Windows レベルおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで事前に有効にする必要があります。  
  
###  <a name="how-to-enable-filestream-at-the-instance-level"></a><a name="HowToFilestream"></a> 方法:インスタンス レベルで FILESTREAM を有効にする  
 FILESTREAM を有効にする方法の詳細については、「 [FILESTREAM の有効化と構成](../../relational-databases/blob/enable-and-configure-filestream.md)」をご覧ください。  
  
 **sp_configure** を呼び出し、FILESTREAM をインスタンス レベルで有効にするには、filestream_access_level オプションを 2 に設定する必要があります。 詳細については、「 [filestream access level サーバー構成オプション](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)」を参照してください。  
  
###  <a name="how-to-allow-filestream-through-the-firewall"></a><a name="firewall"></a> 方法:FILESTREAM がファイアウォールを通過できるようにする  
 FILESTREAM がファイアウォールを通過できるようにする方法については、「 [Configure a Firewall for FILESTREAM Access](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)」をご覧ください。  
  
##  <a name="providing-a-filestream-filegroup-at-the-database-level"></a><a name="filegroup"></a> データベース レベルでの FILESTREAM ファイル グループの指定  
 データベースに FileTable を作成するには、データベースに FILESTREAM ファイル グループが必要です。 この前提条件の詳細については、「 [FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md)」を参照してください。  
  
##  <a name="enabling-non-transactional-access-at-the-database-level"></a><a name="BasicsNTAccess"></a> データベース レベルでの非トランザクション アクセスの有効化  
 FileTable は、Windows アプリケーションがトランザクションを必要とすることなく FILESTREAM データに対する Windows ファイル ハンドルを取得することを可能にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているファイルに対するこの非トランザクション アクセスを可能にするには、FileTable を格納するデータベースごとに、データベース レベルで非トランザクション アクセスのレベルを指定する必要があります。  
  
###  <a name="how-to-check-whether-non-transactional-access-is-enabled-on-databases"></a><a name="HowToCheckAccess"></a> 方法:データベースで非トランザクション アクセスが有効かどうかを確認する  
 カタログ ビュー [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) に対してクエリを実行し、**non_transacted_access** 列と **non_transacted_access_desc** 列をチェックします。  

```sql
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```

###  <a name="how-to-enable-non-transactional-access-at-the-database-level"></a><a name="HowToNTAccess"></a> 方法:データベース レベルで非トランザクション アクセスを有効にする  
 使用できる非トランザクション アクセスのレベルは、FULL、READ_ONLY、および OFF です。  
  
 **Transact-SQL を使用して非トランザクション アクセスのレベルを指定する**  
 - **新しいデータベースを作成**するときに、**NON_TRANSACTED_ACCESS** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) ステートメントを呼び出します。

   ```sql
   CREATE DATABASE database_name  
     WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
   ```

- **既存のデータベースを変更**するときに、**NON_TRANSACTED_ACCESS** FILESTREAM オプションを使用して [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) ステートメントを呼び出します。

   ```sql
   ALTER DATABASE database_name  
     SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
   ```

 **SQL Server Management Studio を使用して非トランザクション アクセスのレベルを指定する**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[オプション]** ページの **[FILESTREAM 非トランザクション アクセス]** ボックスで、非トランザクション アクセスのレベルを指定できます。 このダイアログ ボックスの詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](../../relational-databases/databases/database-properties-options-page.md)」を参照してください。  
  
##  <a name="specifying-a-directory-for-filetables-at-the-database-level"></a><a name="BasicsDirectory"></a> データベース レベルでの FileTable のディレクトリ指定  
 ファイルに対する非トランザクション アクセスをデータベース レベルで有効にする場合、必要に応じて **DIRECTORY_NAME** オプションを使用してディレクトリ名も指定できます。 非トランザクション アクセスを有効にしたときにディレクトリ名を指定しなかった場合は、データベースに FileTable を作成する前にディレクトリ名を指定する必要があります。  
  
 FileTable フォルダー階層において、このデータベース レベルのディレクトリは、インスタンス レベルで FILESTREAM に対して指定された共有名の子になると同時に、データベースに作成された FileTable の親になります。 詳しくは、「 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
###  <a name="how-to-specify-a-directory-for-filetables-at-the-database-level"></a><a name="HowToDirectory"></a> 方法:データベース レベルで FileTable のディレクトリを指定する  
 指定する名前は、データベース レベルで存在するディレクトリに対して一意であることが必要です。  
  
**Transact-SQL を使用して FileTable のディレクトリを指定する**  
- **新しいデータベースを作成**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) ステートメントを呼び出します。

   ```sql
   CREATE DATABASE database_name  
     WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
   GO  
   ```

-   **既存のデータベースを変更**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) ステートメントを呼び出します。 これらのオプションを使用してディレクトリ名を変更するとき、データベースを排他的にロックして、開いているファイル ハンドルがないことを確認する必要があります。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **データベースをアタッチ**するときに、**FOR ATTACH** オプションおよび **DIRECTORY_NAME** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) ステートメントを呼び出します。  
  
    ```sql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **データベースを復元**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントを呼び出します。  
  
    ```sql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **SQL Server Management Studio を使用して、FileTable のディレクトリを指定する**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[オプション]** ページの **[FILESTREAM ディレクトリ名]** ボックスで、ディレクトリ名を指定できます。 このダイアログ ボックスの詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](../../relational-databases/databases/database-properties-options-page.md)」を参照してください。  
  
###  <a name="how-to-view-existing-directory-names-for-the-instance"></a><a name="viewnames"></a> 方法:インスタンスの既存のディレクトリ名を表示する  
 インスタンスの既存のディレクトリ名の一覧を表示するには、[ys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) カタログ ビューに対するクエリを実行し、**filestream_database_directory_name** 列を確認します。  
  
```sql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="requirements-and-restrictions-for-the-database-level-directory"></a><a name="ReqDirectory"></a> データベース レベルのディレクトリの要件と制限  
  
-   **CREATE DATABASE** または **ALTER DATABASE** を呼び出すとき、 **DIRECTORY_NAME**をオプションで設定できます。 **DIRECTORY_NAME**の値を指定しなかった場合、ディレクトリ名は null のままになります。 ただし、データベース レベルで **DIRECTORY_NAME** の値を指定しないと、データベースに FileTable を作成できません。  
  
-   指定するディレクトリ名は、ファイル システムの有効なディレクトリ名に関する要件を満たしている必要があります。  
  
-   データベースに FileTable が含まれている場合、 **DIRECTORY_NAME** を再度 null 値に設定することはできません。  
  
-   データベースをアタッチまたは復元するときに、対象のインスタンスに既に存在する **DIRECTORY_NAME** の値が新しいデータベースにある場合、操作は失敗します。 **CREATE DATABASE FOR ATTACH** または **RESTORE DATABASE** を呼び出すときは、 **DIRECTORY_NAME**に対して一意の値を指定してください。  
  
-   既存のデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードした場合、 **DIRECTORY_NAME** の値は null になります。  
  
-   非トランザクション アクセスをデータベース レベルで有効または無効にするとき、ディレクトリ名が指定されているかどうか、またはディレクトリ名が一意であるかどうかのチェックは行われません。  
  
-   FileTable に対して有効化されていたデータベースを削除すると、データベース レベルのディレクトリとそれ以下のすべての FileTable のすべてのディレクトリ構造が削除されます。  
  
