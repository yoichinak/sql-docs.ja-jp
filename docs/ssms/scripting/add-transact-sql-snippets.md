---
title: Transact-SQL スニペットの追加
description: SQL Server に含まれている定義済みのスニペット一式に、独自の Transact-SQL コード スニペットを追加する方法について学習します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a04c680b5f9753619c0f069ad6c9956bc675cc1
ms.sourcegitcommit: 9e1f1c6ee8f5a10d18a2599bfd9f3eb6081829e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2020
ms.locfileid: "89093566"
---
# <a name="add-transact-sql-snippets"></a>Transact-SQL スニペットの追加

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]には、定義済みの Transact-SQL コード スニペット一式が同梱されていますが、それ以外にも、独自のスニペットを追加することができます。  

## <a name="creating-a-transact-sql-snippet-file"></a>Transact-SQL スニペット ファイルの作成  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] コード スニペットを作成するには、まず、目的のコード スニペットのテキストを含んだ XML ファイルを作成します。 このファイルは、拡張子を .snippet とし、 [コード スニペット スキーマ](https://go.microsoft.com/fwlink/?LinkId=207504)の要件を満たしている必要があります。 スニペットの言語は SQL に設定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属する定義済みのスニペットが参考になります。 定義済みのスニペットを探すには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開いて **[ツール]** メニューを選択し、 **[コード スニペット マネージャー]** をクリックします。 **[言語]** ボックスの一覧の **[SQL]** をクリックすると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スニペットのパスが **[場所]** ボックスに表示されます。  
  
## <a name="registering-the-code-snippet"></a>コード スニペットの登録  
 スニペット ファイルを作成したら、コード スニペット マネージャーを使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]にスニペットを登録します。 複数のスニペットを含んだフォルダーを追加するか、個々のスニペットを **[マイ コード スニペット]** フォルダーにインポートすることができます。  
  
## <a name="procedures"></a>手順  
  
#### <a name="adding-a-snippet-folder"></a>スニペット フォルダーの追加  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[ツール]** メニューを選択し、 **[コード スニペット マネージャー]** をクリックします。  
  
3.  **[追加]** をクリックします。  
  
4.  コード スニペットがあるフォルダーに移動し、 **[フォルダーの選択]** をクリックします。  
  
#### <a name="importing-a-snippet"></a>スニペットのインポート  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[ツール]** メニューを選択し、 **[コード スニペット マネージャー]** をクリックします。  
  
3.  **[Import]\(インポート\)** ボタンをクリックします。  
  
4.  スニペットがあるフォルダーに移動し、.snippet ファイルをクリックして、 **[開く]** をクリックします。  
  
## <a name="examples"></a>例  
 次の例では、 **TRY-CATCH** ブロックの挿入スニペットを作成し、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]にインポートします。  
  
1.  次のコードをメモ帳に貼り付け、TryCatch.snippet というファイル名で保存します。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="https://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
3.  **[ツール]** メニューを選択し、 **[コード スニペット マネージャー]** をクリックします。  
  
4.  **[Import]\(インポート\)** ボタンをクリックします。  
  
5.  TryCatch.snippet があるフォルダーに移動し、TryCatch.snippet ファイルをクリックして、 **[開く]** をクリックします。 これで **[マイ コード スニペット]** フォルダーに既存の TryCatch スニペットが追加されるはずです。  
  
## <a name="see-also"></a>参照  
 [ブロックの挿入 Transact-SQL スニペットの挿入](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
    
