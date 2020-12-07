---
description: RDS のチュートリアル (VBScript)
title: RDS チュートリアル (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ad7fcb2bb63d77bd50c89f11e9b818439b0d1d0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721403"
---
# <a name="rds-tutorial-vbscript"></a>RDS のチュートリアル (VBScript)
これは、Microsoft Visual Basic Scripting Edition で記述された RDS チュートリアルです。 このチュートリアルの目的の詳細については、 [RDS チュートリアル](./rds-tutorial.md)を参照してください。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 このチュートリアルでは、 [RDS.DataControl](../../reference/rds-api/datacontrol-object-rds.md) と [RDS。領域スペース](../../reference/rds-api/dataspace-object-rds.md) はデザイン時に作成されます。つまり、というオブジェクトタグで定義され `<OBJECT>...</OBJECT>` ます。 または、実行時に [CreateObject メソッド (RDS)](../../reference/rds-api/createobject-method-rds.md) メソッドを使用して作成することもできます。 たとえば、RDS のように **なります。DataControl** オブジェクトは次のように作成できます。  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>手順 1-サーバープログラムを指定する  
 VBScript は、VBScript 要求にアクセスすることによって、実行されている IIS Web サーバーの名前を検出できます。 Active Server のページで使用可能な **ServerVariables** メソッドです。  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 ただし、このチュートリアルでは、"サーバー" という架空のサーバーを使用します。  
  
> [!NOTE]
>  **ByRef**引数のデータ型に注意してください。 VBScript を使用して変数の型を指定することはできないため、常に **Variant**を渡す必要があります。 HTTP を使用する場合、rds では、非バリアントを予期しているメソッドに Variant を渡すことができ **ます。領域スペース** オブジェクトの [CreateObject](../../reference/rds-api/createobject-method-rds.md) メソッド。 DCOM またはインプロセスサーバーを使用する場合は、クライアント側とサーバー側でパラメーターの型を一致させる必要があります。一致しない場合は、"型の不一致" エラーが表示されます。  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>手順 2a-RDS を使用してサーバープログラムを起動します。DataControl  
 この例は、RDS の既定の動作を示すコメントにすぎ **ません。DataControl** は、指定されたクエリを実行します。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>手順 2b-RDSServer を使用してサーバープログラムを呼び出す  
  
## <a name="step-3---server-obtains-a-recordset"></a>手順 3-サーバーがレコードセットを取得する  
  
## <a name="step-4---server-returns-the-recordset"></a>手順 4-サーバーがレコードセットを返す  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>手順 5-DataControl をビジュアルコントロールで使用できるようにする  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>手順 6a-RDS を使用してサーバーに変更が送信されます。DataControl  
 この例は、RDS の動作を示すコメントにすぎ **ません。DataControl** は更新を実行します。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>手順 6b-RDSServer を使用してサーバーに変更が送信されます。 DataFactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **これは、チュートリアルの最後です。**  
  
## <a name="see-also"></a>参照  
 [RDS チュートリアル](./rds-tutorial.md)