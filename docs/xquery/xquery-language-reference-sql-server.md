---
title: XQuery 言語リファレンス (SQL Server) |Microsoft Docs
description: SQL Server の XQuery 言語について説明し、完全な言語リファレンスを表示します。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fec2edcca6a5a73c8fcdb9bb0629b7b5ed2ff24
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340463"
---
# <a name="xquery-language-reference-sql-server"></a>XQuery 言語リファレンス (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)] では、 **xml** データ型のクエリに使用される XQuery 言語のサブセットをサポートしています。 この XQuery 実装は、XQuery の2004年7月の作業ドラフトに準拠しています。 この言語は、World Wide Web コンソーシアム (W3C) によって開発されており、すべての主要なデータベースベンダーと Microsoft にも参加しています。 W3c 仕様は W3C 勧告になる前に将来のリビジョンになる可能性があるため、この実装は最終的な推奨事項とは異なる場合があります。 このトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でサポートされる XQuery サブセットのセマンティクスと構文について概説します。  
  
 詳細については、「 [W3C XQuery 1.0 Language Specification](https://go.microsoft.com/fwlink/?LinkId=48846)」を参照してください。  
  
 XQuery は、構造化または半構造化された XML データをクエリできる言語です。 では、 **xml** データ型がサポートされている [!INCLUDE[ssDE](../includes/ssde-md.md)] ため、ドキュメントをデータベースに格納し、XQuery を使用してクエリを実行できます。  
  
 XQuery は、既存の XPath クエリ言語に基づいており、反復処理を改善し、並べ替えの結果を改善し、必要な XML を構築する機能が追加されました。 XQuery は XQuery データ モデルで動作します。 これは、XML ドキュメントの抽象化と、型指定または型指定ができない XQuery 結果です。 型情報は W3C XML Schema 言語によって提供される型に基づきます。 使用できる入力情報がない場合、XQuery はデータを型指定されていないものとして処理します。 これは、XPath バージョン1.0 が XML を処理する方法に似ています。  
  
 **Xml 型の** 変数または列に格納されている xml インスタンスに対してクエリを実行するには、 [xml データ型のメソッド](../t-sql/xml/xml-data-type-methods.md)を使用します。 たとえば、 **xml 型の** 変数を宣言し、 **xml** データ型の **query ()** メソッドを使用してクエリを実行することができます。  
  
```sql
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 次の例では、AdventureWorks データベースの ProductModel テーブルの **xml** 型の命令列に対してクエリを指定しています。  
  
```sql
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 XQuery には、名前空間宣言、 `declare namespace``AWMI=...` 、およびクエリ式 () が含まれてい `/AWMI:root/AWMI:Location[@LocationID=10]` ます。  
  
 XQuery は、 **xml** 型の命令列に対して指定されていることに注意してください。 Xml データ型の [query () メソッド](../t-sql/xml/query-method-xml-data-type.md) は、XQuery を指定するために使用されます。  
  
 次の表は、[!INCLUDE[ssDE](../includes/ssde-md.md)]での XQuery の実装を理解する際に役立つ関連トピックを示しています。  
  
|トピック|説明|  
|-----------|-----------------|  
|[XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|での **xml** データ型のサポート [!INCLUDE[ssDE](../includes/ssde-md.md)] と、このデータ型に対して使用できるメソッドについて説明します。 **Xml** データ型は、xquery 式が実行される入力 xquery データモデルを形成します。|  
|[XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|データベースに格納されている XML インスタンスを型指定する方法について説明します。 これは、xml スキーマコレクションを **xml** 型の列に関連付けることができることを意味します。 列に格納されているすべてのインスタンスは、コレクション内のスキーマに対して検証および型指定され、XQuery の型情報を提供します。|  
|||  
  
> [!NOTE]  
>  このセクションの構成は、W3C (World Wide Web Consortium) XQuery ワーキング ドラフト仕様に基づいています。 このセクションで提供する図の一部は、その仕様から引用したものです。 このセクションでは、Microsoft XQuery の実装と w3c 仕様を比較し、Microsoft XQuery が W3C とどのように異なるかを説明し、サポートされていない W3C 機能について説明します。 W3C 仕様は、で入手でき [http://www.w3.org/TR/2004/WD-xquery-20040723](https://go.microsoft.com/fwlink/?LinkId=48846) ます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[XQuery の基礎](../xquery/xquery-basics.md)|XQuery の概念の基本的な概要と、式の評価 (静的および動的コンテキスト)、アトミック化、有効なブール値、XQuery 型システム、シーケンス型の照合、およびエラー処理について説明します。|  
|[XQuery 式](../xquery/xquery-expressions.md)|XQuery 原始式、パス式、シーケンス式、算術式、比較式、論理式、XQuery の構築、FLWOR 式、条件式、量化式、およびシーケンス型のさまざまな式について説明します。|  
|[XQuery&#41;&#40;モジュールと Prologs ](../xquery/modules-and-prologs-xquery.md)|XQuery プロローグについて説明します。|  
|[xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)|サポートされている XQuery 関数の一覧について説明します。|  
|[xml データ型に対する XQuery の演算子](../xquery/xquery-operators-against-the-xml-data-type.md)|サポートされている XQuery 演算子について説明します。|  
|[xml データ型に対する XQuery のその他のサンプル](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|XQuery の追加サンプルを提供します。|  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
