---
description: VBScript での ADO プログラミング
title: VBScript ADO プログラミング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b89d247f5bc91ca0b3494c15d3781116b8c9614
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990923"
---
# <a name="vbscript-ado-programming"></a>VBScript での ADO プログラミング
## <a name="creating-an-ado-project"></a>ADO プロジェクトの作成  
 Microsoft Visual Basic Scripting Edition では、タイプライブラリがサポートされていないため、プロジェクトで ADO を参照する必要はありません。 そのため、コマンドライン補完などの関連する機能はサポートされません。 また、既定では、ADO の列挙定数は VBScript で定義されていません。  
  
 ただし、ADO には、VBScript で使用する次の定義を含む2つのインクルードファイルが用意されています。  
  
-   サーバー側スクリプトでは、Adovbs を使用します。これは、既定で c:\Program Files\Common Files\System\ado\ フォルダーにインストールされます。  
  
-   クライアント側スクリプトの場合は、既定で c:\Program Files\Common Files\System\msdac\ フォルダーにインストールされている Adcvbs. inc. を使用します。  
  
 これらのファイルの定数定義をコピーして ASP ページに貼り付けるか、サーバー側スクリプトを実行している場合は、Adovbs ファイルを Web サイトのフォルダーにコピーして、次のように ASP ページから参照できます。  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>VBScript での ADO オブジェクトの作成  
 **Dim**ステートメントを使用して、VBScript の特定の型にオブジェクトを割り当てることはできません。 また、VBScript では、Visual Basic for Applications の**Dim**ステートメントで使用される**新しい**構文はサポートされていません。 代わりに、 **CreateObject** 関数の呼び出しを使用する必要があります。  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript の例  
 次のコードは、Active Server ページ (ASP) ファイルでの VBScript サーバー側プログラミングの一般的な例です。  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 ADO ドキュメントには、より具体的な VBScript の例が含まれています。 詳細については、「 [Microsoft Visual Basic Scripting Edition の ADO コード例](../../reference/ado-api/ado-code-examples-vbscript.md)」を参照してください。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript と Visual Basic の違い  
 VBScript での ADO の使用は、構文の使用方法など、さまざまな方法で Visual Basic ADO を使用する場合と似ています。 ただし、いくつかの重要な違いがあります。  
  
-   VBScript は、さまざまな種類のデータを保持できる Variant データ型のみをサポートしています。 必要なデータをバリアントデータ型に格納すると、VBScript によって実行されるキャストによってデータが適切に機能します。 ADO が必要とする型を認識し、それに応じてバリアントの値を変換します。  
  
-   VBScript 内で**on error goto \<label> **を使用することはできません。  
  
-   VBScript では、 **Msgbox**、 **Date**、 **IsNumeric**などの組み込みの Visual Basic 関数の一部がサポートされています。 ただし、VBScript は Visual Basic のサブセットであるため、一部の組み込み関数はサポートされていません。 たとえば、VBScript では **Format** 関数とファイル i/o 関数はサポートされていません。