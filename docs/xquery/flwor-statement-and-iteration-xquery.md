---
title: FLWOR ステートメントと繰り返し (XQuery) |Microsoft Docs
description: XQuery で FLOWR イテレーション構文を構成する for、let、where、order by、および return 句について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
ms.openlocfilehash: daca777a2994813a6df131d1fa756edf4f753f6e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100353314"
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR ステートメントと繰り返し (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery では、FLWOR 反復構文が定義されています。 FLWOR とは、`for`、`let`、`where`、`order by`、および `return` の頭文字です。  
  
 FLWOR ステートメントは、次の部分で構成されています。  
  
-   1つ以上の反復子変数を入力シーケンスにバインドする1つ以上の FOR 句。  
  
     入力シーケンスは、XPath 式などの他の XQuery 式にすることができます。 これらは、ノードのシーケンスまたはアトミック値のシーケンスです。 アトミック値のシーケンスは、リテラルまたはコンストラクター関数を使用して作成できます。 では、構築された XML ノードを入力シーケンスとして使用することはできません [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
-   省略可能な `let` 句。 この句は、特定の繰り返し処理の変数に値を割り当てます。 割り当てられた式は、XPath 式などの XQuery 式にすることができ、ノードのシーケンスまたはアトミック値のシーケンスのいずれかを返すことができます。 アトミック値のシーケンスは、リテラルまたはコンストラクター関数を使用して作成できます。 では、構築された XML ノードを入力シーケンスとして使用することはできません [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
-   反復子変数。 この変数は、キーワードを使用してオプションの型アサーションを持つことができ `as` ます。  
  
-   省略可能な `where` 句。 繰り返しにフィルター述語を適用します。  
  
-   省略可能な `order by` 句。  
  
-   `return` 式。 句内の式は、 `return` FLWOR ステートメントの結果を構築します。  
  
 たとえば、次のクエリでは、 `Step` 最初の製造場所の <> 要素を反復処理し、<> ノードの文字列値を返し `Step` ます。  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 結果を次に示します。  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 次のクエリは前のクエリと似ていますが、ProductModel テーブルの型指定された xml 列である命令列に対して指定されている点が異なります。 このクエリは、 `step` 特定の製品の最初のワークセンターの場所で、> 要素を <すべての製造手順を反復処理します。  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `$Step` は反復子変数です。  
  
-   [パス式](../xquery/path-expressions-xquery.md)では、 `//AWMI:root/AWMI:Location[1]/AWMI:step` 入力シーケンスが生成されます。 このシーケンスは、 `step` 最初の <> 要素ノードの子 <> 要素ノードのシーケンスです `Location` 。  
  
-   省略可能な述語句 `where` は使用しません。  
  
-   式は、 `return` <> 要素から文字列値を返し `step` ます。  
  
 [文字列関数 (XQuery)](../xquery/data-accessor-functions-string-xquery.md)は、<> ノードの文字列値を取得するために使用され `step` ます。  
  
 結果の一部を次に示します。  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 許可される追加の入力シーケンスの例を次に示します。  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では異種シーケンスが許可されていません。 具体的には、アトミック値とノードが混在しているシーケンスは許可されません。  
  
 反復は、次のクエリで示すように XML 形式の変換で [Xml 構築](../xquery/xml-construction-xquery.md) 構文と一緒に使用されることがよくあります。  
  
 AdventureWorks サンプルデータベースでは、 **Production モデル** テーブルの **命令** 列に格納されている製造手順の形式は次のとおりです。  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 次のクエリでは、 `Location` 子要素として返されるワークセンターの場所の属性を持つ <> 要素を持つ新しい XML が構築されます。  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 クエリは次のとおりです。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   FLWOR ステートメントは、特定の製品の <> 要素のシーケンスを取得し `Location` ます。  
  
-   [Data 関数 (XQuery)](../xquery/data-accessor-functions-data-xquery.md)は、各属性の値を抽出するために使用されます。これにより、属性としてではなく、結果の XML にテキストノードとして追加されます。  
  
-   RETURN 句の式で、必要な XML を生成します。  
  
 結果の一部を次に示します。  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>Let 句の使用  
 句を使用すると、 `let` 変数を参照して参照できる反復式に名前を指定できます。 `let` 変数に割り当てられた式は、変数がクエリ内で参照されるたびにクエリに挿入されます。 これは、ステートメントが、式が参照される回数だけ実行されることを意味します。  
  
 データベースでは、製造手順には、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 必要なツールとツールが使用されている場所に関する情報が含まれています。 次のクエリは、`let` 句を使用して、製品モデルの作成に必要なツールと、それぞれのツールが必要となる場所を一覧表示します。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>where 句の使用  
 句を使用して、 `where` イテレーションの結果をフィルター処理できます。 このことを次の例で説明します。  
  
 自転車の製造では、製造プロセスは一連のワークセンターの場所を通過します。 各ワークセンターの場所では、製造手順の順序を定義します。 次のクエリでは、自転車モデルを製造し、製造手順が3つ未満のワークセンターの場所のみを取得します。 つまり、3つの <> 要素を持つことになり `step` ます。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `where`キーワードは **count ()** 関数を使用して、 `step` 各ワークセンターの場所の <> 子要素の数をカウントします。  
  
-   式は、 `return` イテレーションの結果から必要な XML を構築します。  
  
 結果を次に示します。  
  
```  
<Location LocationID="30"/>   
```  
  
 `where` 句内の式の結果は、次の規則を順に適用してブール値に変換されます。 これらは、パス式の述語の規則と同じですが、整数は使用できません。  
  
1.  式が `where` 空のシーケンスを返す場合、その有効なブール値は False になります。  
  
2.  `where` 式が単純な Boolean 型の値を 1 つ返す場合、その値が有効なブール値になります。  
  
3.  式が、 `where` 少なくとも1つのノードを含むシーケンスを返す場合、有効なブール値は True になります。  
  
4.  それ以外の場合は、静的エラーが発生します。  
  
## <a name="multiple-variable-binding-in-flwor"></a>FLWOR での複数の変数のバインド  
 1 つの FLWOR 式で入力シーケンスに複数の変数をバインドできます。 次の例では、型指定されていない xml 変数に対してクエリを指定しています。 FLOWR 式は、 `Step` 各 <> 要素の最初の <> 要素の子を返し `Location` ます。  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   式では `for` 、$ variables が定義されて `$Loc` `FirstStep` います。  
  
-   `two`式、およびは、 `/ManuInstructions/Location` `$FirstStep in $Loc/Step[1]` の値がの値に依存するということに関連付けられてい `$FirstStep` `$Loc` ます。  
  
-   に関連付けられた式は、 `$Loc` 一連の <> 要素を生成し `Location` ます。 各 <> 要素について `Location` 、は `$FirstStep` 1 つの <`Step`> 要素 (シングルトン) のシーケンスを生成します。  
  
-   `$Loc` は、変数に関連付けられた式で指定され `$FirstStep` ます。  
  
 結果を次に示します。  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 次のクエリは似ていますが、 **Productmodel** テーブルの、型指定された **xml** 列である命令列に対して指定されている点が異なります。 [Xml の構築 (XQuery)](../xquery/xml-construction-xquery.md) は、必要な xml を生成するために使用されます。  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `for` 句で 2 つの変数 `$WC` および `$S` を定義します。 `$WC` に関連付けられた式により、ある製造モデルの自転車の製造で使用されるワーク センター拠点のシーケンスが生成されます。 `$S` 変数に代入されたパス式は、`$WC` で示すワーク センター拠点のシーケンスごとに製造手順のシーケンスを生成します。  
  
-   Return ステートメントは、 `Step` 製造手順と **locationid** を属性として含む <> 要素を持つ XML を構築します。  
  
-   **既定の declare 要素の名前空間** は、結果の XML 内のすべての名前空間宣言が最上位の要素に表示されるように、XQuery プロローグで使用されます。 これにより、結果が読みやすくなります。 既定の名前空間の詳細については、「 [XQuery での名前空間の処理](../xquery/handling-namespaces-in-xquery.md)」を参照してください。  
  
 結果の一部を次に示します。  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>Order by 句の使用  
 XQuery での並べ替えは、FLWOR 式の句を使用して実行され `order by` ます。 句に渡される並べ替え式は、 `order by` **gt** 演算子に対して有効な型を持つ値を返す必要があります。 各並べ替え式は、1つの項目を持つ単一のシーケンスになる必要があります。 既定では、並べ替えは昇順で実行されます。 必要に応じて、並べ替え式ごとに昇順または降順を指定することもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に実装された XQuery で行う、文字列値を並べ替えるための比較には、常にバイナリの Unicode コード ポイントの照合順序が使用されます。  
  
 次のクエリでは、AdditionalContactInfo 列から特定の顧客のすべての電話番号を取得します。 結果は電話番号順に並べ替えます。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 [アトミック化 (XQuery)](../xquery/atomization-xquery.md)プロセスは、 `number` に渡す前に <> 要素のアトミック値を取得することに注意して `order by` ください。 式は **data ()** 関数を使用して記述できますが、必須ではありません。  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 結果を次に示します。  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 名前空間は、クエリのプロローグではなく WITH XMLNAMESPACES でも宣言できます。  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 属性値で並べ替えることもできます。 たとえば、次のクエリは、新しく作成された <> 要素を取得し `Location` ます。この要素には、LocationID 属性と LaborHours 属性が LaborHours 属性によって降順で並べ替えられています。 その結果、最大労働時間があるワークセンターの場所が最初に返されます。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 結果を次に示します。  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 次のクエリは、結果を要素名順に並べ替えます。 このクエリは、製品カタログから特定の製品の仕様を取得します。 仕様は、<> 要素の子です `Specifications` 。  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `/p1:ProductDescription/p1:Specifications/*`式は <> の子要素を返し `Specifications` ます。  
  
-   式は、 `order by (local-name($a))` 要素名のローカル部分でシーケンスを並べ替えます。  
  
 結果を次に示します。  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 順序付け式が空を返すノードは、次の例に示すように、シーケンスの先頭に並べ替えられます。  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 結果を次に示します。  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 次の例に示すように、複数の並べ替え条件を指定できます。 この例のクエリでは、 `Employee` 最初にタイトル、次に管理者属性値によって <> 要素を並べ替えます。  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 結果を次に示します。  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   並べ替え式では、型を混在させないようにする必要があります。 これは静的にチェックされます。  
  
-   空のシーケンスの並べ替えは制御できません。  
  
-   `order by` ではキーワード empty least、empty greatest、および collation を使用できません。  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
