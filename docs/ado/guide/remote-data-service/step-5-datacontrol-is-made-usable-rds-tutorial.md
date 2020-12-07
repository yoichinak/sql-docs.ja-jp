---
description: 手順 5:DataControl が使用可能になる (RDS チュートリアル)
title: '手順 5: DataControl を使用できるようになりました (RDS チュートリアル) |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 560c5968b3343f2553bc117ebbbdcf06938cc49f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722953"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>手順 5:DataControl が使用可能になる (RDS チュートリアル)
返された **レコードセット** オブジェクトを使用できます。 他の **レコードセット**と同じように、確認、移動、または編集を行うことができます。 **レコードセット**でできることは、環境によって異なります。 Visual Basic と Visual C++ には、データコントロールを有効にすることで、直接または間接的に **レコードセット** を使用できるビジュアルコントロールがあります。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 たとえば、Microsoft Internet Explorer で Web ページを表示している場合、 **レコードセット** オブジェクトのデータをビジュアルコントロールに表示することができます。 Web ページ上のビジュアルコントロールは、 **レコードセット** オブジェクトに直接アクセスできません。 ただし、これらのユーザーは、RDS を介して **レコードセット** オブジェクトにアクセスでき [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md)。 **RDS。DataControl**は、 [SourceRecordset](../../reference/rds-api/recordset-sourcerecordset-properties-rds.md)プロパティが**レコードセット**オブジェクトに設定されている場合に、ビジュアルコントロールによって使用できるようになります。  
  
 ビジュアルコントロールオブジェクトは、 **DATASRC** パラメーターを RDS に設定する必要があり **ます。DataControl**とその **DATAFLD** プロパティは、 **レコードセット** オブジェクトフィールド (列) に設定されています。  
  
 このチュートリアルでは、 **SourceRecordset** プロパティを次のように設定します。  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>参照  
 [手順 6: 変更がサーバーに送信される (RDS チュートリアル)](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)