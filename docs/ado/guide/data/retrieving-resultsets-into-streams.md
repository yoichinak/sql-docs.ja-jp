---
description: ストリーム形式で結果セットを取得する
title: 結果セットをストリームに取得する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: rothja
ms.author: jroth
ms.openlocfilehash: 13aeddcf9a826cff5caa33172f785f2e42747a3f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979753"
---
# <a name="retrieving-resultsets-into-streams"></a>ストリーム形式で結果セットを取得する
ADO では、従来の **Recordset** オブジェクトの結果を受け取る代わりに、クエリの結果をストリームに取得できます。 ADO**ストリーム**オブジェクト (または、ASP**要求**オブジェクトや**応答**オブジェクトなど、COM **IStream**インターフェイスをサポートするその他のオブジェクト) は、これらの結果を格納するために使用できます。 この機能の使用方法の1つは、結果を XML 形式で取得することです。 たとえば、SQL Server では、XML の結果を複数の方法で返すことができます。たとえば、SQL SELECT クエリで FOR XML 句を使用する場合や、XPath クエリを使用する場合などです。  
  
 **レコードセット**ではなくストリーム形式でクエリ結果を受け取るには、 **executeoptionenum**から**adExecuteStream**定数を**Command**オブジェクトの**Execute**メソッドのパラメーターとして指定する必要があります。 プロバイダーがこの機能をサポートしている場合、結果は実行時にストリームで返されます。 コードを実行する前に、追加のプロバイダー固有のプロパティを指定する必要がある場合があります。 たとえば、Microsoft OLE DB Provider for SQL Server では、 **Command**オブジェクトの**properties**コレクション内の**出力ストリーム**などのプロパティを指定する必要があります。 この機能に関連する SQL Server 固有の動的プロパティの詳細については、SQL Server オンラインブックの「XML 関連のプロパティ」を参照してください。  
  
## <a name="for-xml-query-example"></a>FOR XML クエリの例  
 次の例は、VBScript で Northwind データベースに記述されています。  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 FOR XML 句は、XML ドキュメントの形式でデータを返すように SQL Server に指示します。  
  
### <a name="for-xml-syntax"></a>FOR XML 構文  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW は、属性として列値を持つ汎用の行要素を生成します。 FOR XML AUTO では、ヒューリスティックを使用して、テーブル名に基づいて要素名を持つ階層ツリーが生成されます。 FOR XML EXPLICIT では、メタデータによって完全に記述されたリレーションシップを持つユニバーサルテーブルが生成されます。  
  
 SQL SELECT FOR XML ステートメントの例を次に示します。  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 コマンドは、前に示した文字列、 **CommandText**に割り当てられた文字列、または **commandstream**に割り当てられた XML テンプレートクエリの形式で指定できます。 XML テンプレートクエリの詳細については、「ADO の [コマンドストリーム](../../../ado/guide/data/command-streams.md) 」または「SQL Server オンラインブックでのコマンド入力用ストリームの使用」を参照してください。  
  
 XML テンプレートクエリとして、FOR XML クエリは次のように表示されます。  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 この例では、**出力ストリーム**プロパティの ASP**応答**オブジェクトを指定します。  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 次に、 **Execute**の**adExecuteStream**パラメーターを指定します。 この例では、xml タグでストリームをラップして XML データアイランドを作成します。  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>解説  
 この時点で、XML がクライアントブラウザーにストリームされ、表示されるようになります。 これを行うには、クライアント側の VBScript を使用して XML ドキュメントを DOM のインスタンスにバインドし、各子ノードをループして HTML で製品の一覧を作成します。
