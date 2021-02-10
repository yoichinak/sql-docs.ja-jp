---
description: JScript での ADO プログラミング
title: JScript ADO プログラミング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: rothja
ms.author: jroth
ms.openlocfilehash: 15a58e69810e3df5221d4c869e14b20112a181c9
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100029416"
---
# <a name="jscript-ado-programming"></a>JScript での ADO プログラミング
## <a name="creating-an-ado-project"></a>ADO プロジェクトの作成  
 Microsoft JScript では、タイプライブラリがサポートされていないため、プロジェクトで ADO を参照する必要はありません。 そのため、コマンドライン補完などの関連する機能はサポートされません。 また、既定では、ADO の列挙定数は JScript で定義されていません。  
  
 ただし、ADO には、JScript で使用する次の定義を含む2つのインクルードファイルが用意されています。  
  
-   サーバー側スクリプトを使用する場合は、Adojavas を使用します。これは ADO library フォルダーにインストールされます。  
  
-   クライアント側スクリプトの場合は、Adcjavas を使用します。これは ADO library フォルダーにインストールされます。  
  
 これらのファイルの定数定義をコピーして ASP ページに貼り付けるか、サーバー側スクリプトを実行する場合は、Adojavas ファイルを Web サイトのフォルダーにコピーして、次のように ASP ページから参照できます。  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>JScript での ADO オブジェクトの作成  
 代わりに、 **CreateObject** 関数の呼び出しを使用する必要があります。  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript の例  
 次のコードは、 **レコードセット** オブジェクトを開く Active Server ページ (ASP) ファイルでの JScript のサーバー側プログラミングの一般的な例です。  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
