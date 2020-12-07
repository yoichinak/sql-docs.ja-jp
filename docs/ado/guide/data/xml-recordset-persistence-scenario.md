---
description: XML レコードセットの保持シナリオ
title: XML レコードセット永続化シナリオ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: rothja
ms.author: jroth
ms.openlocfilehash: 91066d8dd42d1bcd4a11aab093661a9061a7d7d1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978823"
---
# <a name="xml-recordset-persistence-scenario"></a>XML レコードセットの保持シナリオ
このシナリオでは、レコードセットオブジェクトの内容を ASP 応答オブジェクトに直接保存する Active Server Pages (ASP) アプリケーションを作成します。  
  
> [!NOTE]
>  このシナリオでは、サーバーにインターネットインフォメーションサーバー 5.0 (IIS) 以降がインストールされている必要があります。  
  
 返されたレコードセットは、Internet Explorer の [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)を使用して表示されます。  
  
 このシナリオを作成するには、次の手順を実行する必要があります。  
  
-   アプリケーションを設定する  
  
-   データを取得する  
  
-   データを送信する  
  
-   データの受信と表示  
  
## <a name="step-1-set-up-the-application"></a>手順 1: アプリケーションをセットアップする  
 スクリプト権限を使用して、"XMLPersist" という名前の IIS 仮想ディレクトリを作成します。 仮想ディレクトリが指すフォルダーに、"XMLResponse .asp" という名前の2つの新しいテキストファイルを作成します。 "Default.htm" という名前を付けます。  
  
## <a name="step-2-get-the-data"></a>手順 2: データを取得する  
 この手順では、ADO レコードセットを開いてクライアントに送信するための準備を行うコードを記述します。 ファイル XMLResponse .asp をメモ帳などのテキストエディターで開き、次のコードを挿入します。  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 のパラメーターの値は、必ず `Data Source` `strCon` Microsoft SQL Server コンピューターの名前に変更してください。  
  
 ファイルを開いたままにして、次の手順に進みます。  
  
## <a name="step-3-send-the-data"></a>手順 3: データを送信する  
 レコードセットを取得したので、それをクライアントに送信する必要があります。これは、XML として ASP 応答オブジェクトに保存することによって行います。 XMLResponse. asp の下に次のコードを追加します。  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 ASP 応答オブジェクトが、レコードセットの [保存方法](../../reference/ado-api/save-method.md)の送信先として指定されていることに注意してください。 Save メソッドの送信先には、IStream インターフェイスをサポートする任意のオブジェクト [(Ado ストリームオブジェクト (ado) など)](../../reference/ado-api/stream-object-ado.md)、またはレコードセットを保存する完全なパスを含むファイル名を指定できます。  
  
 次の手順に進む前に、XMLResponse .asp を保存して閉じます。 また、adovbs ファイルを既定の ADO ライブラリインストールフォルダーから、XMLResponse .asp ファイルを保存したフォルダーにコピーします。  
  
## <a name="step-4-receive-and-display-the-data"></a>手順 4: データを受信して表示する  
 この手順では、レコードセットを取得するために XMLResponse. .asp ファイルをポイントする埋め込みの [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md) オブジェクトを含む HTML ファイルを作成します。 メモ帳などのテキストエディターを使用して default.htm を開き、次のコードを追加します。 URL の "sqlserver" をサーバーの名前に置き換えます。  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 default.htm ファイルを閉じ、XMLResponse .asp を保存したフォルダーに保存します。 Internet Explorer 4.0 以降を使用して、https://*sqlserver*/xmlpersist/default.htm URL を開き、結果を確認します。 データは、バインドされた DHTML テーブルに表示されます。 ここで、https:// *sqlserver* /XMLPersist/XMLResponse.asp という URL を開き、結果を確認します。 XML が表示されます。  
  
## <a name="see-also"></a>参照  
 [Save メソッド](../../reference/ado-api/save-method.md)   
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)