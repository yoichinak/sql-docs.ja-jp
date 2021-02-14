---
title: 式のコンテキストとクエリの評価 (XQuery) |Microsoft Docs
description: XQuery 式の静的コンテキストと動的コンテキストからの情報を分析および評価するために使用する方法について説明します。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: f4fd85737d1a7cdc981576f624a2a403f0eb19ee
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341954"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>式コンテキストとクエリの評価 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  式のコンテキストは、式の分析と評価を行うために使用される情報です。 次に、XQuery を評価する際の 2 つのフェーズを示します。  
  
-   **静的コンテキスト** -これは、クエリのコンパイルフェーズです。 使用可能な情報に基づいて、クエリのこの静的分析中にエラーが発生することがあります。  
  
-   **動的コンテキスト** -これはクエリ実行フェーズです。 クエリをコンパイル中のエラーなどの静的エラーが含まれない場合でも、クエリの実行中にエラーが返ることがあります。  
  
## <a name="static-context"></a>静的コンテキスト  
 静的コンテキストの初期化とは、式の静的分析向けに、すべての情報をまとめるプロセスのことです。 静的コンテキストの初期化の一環として、次のことが行われます。  
  
-   **境界の空白文字** のポリシーがストリップに設定されています。 このため、境界の空白は、クエリ内の **要素** および **属性** のコンストラクターによって保持されません。 次に例を示します。  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     XQuery 式の解析時に境界空白文字が取り除かれるので、このクエリは次の結果を返します。  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   プレフィックスと名前空間のバインドは、次のように初期化されます。  
  
    -   事前定義済みの一連の名前空間。  
  
    -   WITH XMLNAMESPACES を使用して定義されたすべての名前空間。 詳細については、「 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」を参照してください。  
  
    -   クエリのプロローグに定義されているすべての名前空間。 プロローグ内の名前空間宣言により、WITH XMLNAMESPACES で名前空間宣言がオーバーライドされる場合があることに注意してください。 たとえば、次のクエリでは、WITH XMLNAMESPACES で名前空間 () にバインドするプレフィックス (pd) が宣言されて `https://someURI` います。 ただし、WHERE 句では、バインドよりもクエリのプロローグがオーバーライドされます。  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     これらすべての名前空間のバインドは、静的コンテキストの初期化時に解決されます。  
  
-   型指定された **xml** 列または変数に対してクエリを実行する場合は、列または変数に関連付けられている xml スキーマコレクションのコンポーネントが静的コンテキストにインポートされます。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
-   インポートされたスキーマのすべてのアトミック型についても、キャスト関数が静的コンテキストで使用可能になります。 このことを次の例で説明します。 この例では、型指定された **xml** 変数に対してクエリを指定しています。 この変数に関連付けられている XML スキーマ コレクションでは、アトミック型である myType が定義されています。 この型に対応する、キャスト関数 **myType ()** は、スタティック分析中に使用できます。 クエリ式 () は、 `ns:myType(0)` myType の値を返します。  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     次の例では、 **int** 組み込み XML 型のキャスト関数が式で指定されています。  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 静的コンテキストが初期化されると、クエリ式が分析 (コンパイル) されます。 静的分析には、次のものが含まれます。  
  
1.  クエリの解析。  
  
2.  式で指定された関数と型名を解決します。  
  
3.  クエリの静的な型指定。 これにより、クエリがタイプ セーフであることを確認できます。 たとえば、次のクエリは静的エラーを返し **+** ます。演算子には数値のプリミティブ型引数が必要であるためです。  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     次の例では、 **value ()** 演算子にシングルトンが必要です。 XML スキーマで指定されているように、複数の要素が存在する場合があり \<Elem> ます。 式の静的な分析によって、型が安全でないと判断され、静的エラーが返されます。 エラーを解決するには、単一の結果になることを明示的に指定するように (`data(/x:Elem)[1]`)、式を書き直す必要があります。  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     詳細については、「 [XQuery と静的](../xquery/xquery-and-static-typing.md)な型指定」を参照してください。  
  
### <a name="implementation-restrictions"></a>実装の制限  
 次に、静的コンテキストに関する制限事項を示します。  
  
-   XPath 互換モードはサポートされていません。  
  
-   XML の構築では、ストリップ構築モードのみがサポートされています。 これは、既定の設定です。 したがって、構築された要素ノードの型は **xdt:** 型指定されていない型で、属性は **Xdt: untypedAtomic** 型です。  
  
-   順序付けされた順序付けモードのみがサポートされています。  
  
-   XML 空間の削除ポリシーのみがサポートされています。  
  
-   ベース URI 機能はサポートされていません。  
  
-   **fn: doc ()** はサポートされていません。  
  
-   **fn: collection ()** はサポートされていません。  
  
-   XQuery の静的フラグが指定されていません。  
  
-   **Xml** データ型に関連付けられている照合順序が使用されます。 この照合順序は、常に Unicode コードポイント照合順序に設定されます。  
  
## <a name="dynamic-context"></a>動的コンテキスト  
 動的コンテキストとは、式の実行時に使用できる必要のある情報のことです。 静的コンテキストに加えて、次の情報は動的コンテキストの一部として初期化されます。  
  
-   次に示すように、式のフォーカス (コンテキスト項目、コンテキストの位置、コンテキストのサイズなど) が初期化されます。 これらの値はすべて [nodes () メソッド](../t-sql/xml/nodes-method-xml-data-type.md)でオーバーライドできることに注意してください。  
  
    -   **Xml** データ型は、処理対象のノードであるコンテキスト項目をドキュメントノードに設定します。  
  
    -   コンテキストの位置 (処理されているノードに対するコンテキスト項目の相対的な位置) は、最初に1に設定されます。  
  
    -   コンテキストサイズ (処理されているシーケンス内の項目の数) は、常に1に設定されます。これは、ドキュメントノードが常に1つあるためです。  
  
### <a name="implementation-restrictions"></a>実装の制限  
 次に、動的コンテキストに関する制限事項を示します。  
  
-   **現在の日付と時刻** のコンテキスト関数 ( **fn: current-date**、 **fn: current time**、および **fn: current-dateTime**) はサポートされていません。  
  
-   **暗黙のタイムゾーン** は UTC + 0 に固定されており、変更することはできません。  
  
-   **Fn: doc ()** 関数はサポートされていません。 すべてのクエリは、 **xml** 型の列または変数に対して実行されます。  
  
-   **Fn: collection ()** 関数はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
