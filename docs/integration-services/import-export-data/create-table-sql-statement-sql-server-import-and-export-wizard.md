---
description: '[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード)'
title: '[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7854a8121c16d263da900ffc3f8475a4fe4dddff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484138"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


**[変換先テーブルを作成する]** を選択してから **[列マッピング]** ダイアログ ボックスで **[SQL の編集]** を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードに **[テーブル作成 SQL ステートメント]** ダイアログ ボックスが表示されます。 このページでは、 **CREATE TABLE** コマンドを確認し、必要に応じてカスタマイズします。このコマンドは、新しいターゲット テーブルを作成するためにウィザードで実行されます。
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの **[テーブル作成 SQL ステートメント]** ダイアログ ボックスではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE ステートメントに関する情報をお探しの場合は、「[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>[CREATE TABLE SQL ステートメント] ページのスクリーン ショット  
 以下のスクリーン ショットには、ウィザードの **[テーブル作成 SQL ステートメント]** ダイアログ ボックスが示されています。
 
この例では、 **[SQL ステートメント]** ボックスに、ウィザードで生成される既定の **CREATE TABLE** ステートメントが含まれています。 このステートメントにより、**Person.Address** ソース テーブルのコピーである **Person.Address** という名前の新しい変換先テーブルが作成されます。 
  
 ![インポートおよびエクスポート ウィザードの [テーブルの作成] ページ](../../integration-services/import-export-data/media/create-table.png "インポートおよびエクスポート ウィザードの [テーブルの作成] ページ")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>CREATE TABLE ステートメントの確認または再生成  
 **SQL ステートメント**  
自動生成された SQL ステートメントが表示され、編集できます。
 
既定の CREATE TABLE コマンドを変更する場合は、**[列マッピング]** ダイアログ ボックスに戻るときに、関連付けられている列マッピングの変更が必要になることもあります。  
  
SQL ステートメントのテキストにキャリッジ リターンを含めるには、Ctrl キーを押しながら Enter キーを押します。 Enter キーだけを押すと、ダイアログ ボックスが閉じます。  
  
CREATE TABLE ステートメントと構文の詳細については、「[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。   
  
 **自動生成**  
 **[自動生成]** をクリックすると、既定の SQL ステートメントを変更していた場合、復元されます。  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>FILESTREAM 列を含むテーブルの作成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードにより、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 ソース テーブルに FILESTREAM 列がある場合でも、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。
 1.  ウィザードを使用して FILESTREAM 列をコピーするには、まず、対象データベースに FILESTREAM ストレージを実装します。
 2.  次に、 **[テーブル作成 SQL ステートメント]** ダイアログ ボックスで CREATE TABLE ステートメントに手動で FILESTREAM 属性を追加します。  

構文の詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。 FILESTREAM の詳細については、「[バイナリ ラージ オブジェクト (Blob) データ (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
## <a name="whats-next"></a>次の手順  
 CREATE TABLE コマンドを確認し、カスタマイズしてから **[OK]** をクリックすると、 **[テーブル作成 SQL ステートメント]** ダイアログ ボックスから **[列マッピング]** ダイアログ ボックスに戻ります。 詳細については、「 [列マッピング](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)」を参照してください。
 
 ## <a name="see-also"></a>関連項目
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


