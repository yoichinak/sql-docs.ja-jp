---
description: 手順 1:サーバー プログラムを指定する (RDS チュートリアル)
title: '手順 1: サーバープログラムを指定する (RDS チュートリアル) |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: rothja
ms.author: jroth
ms.openlocfilehash: 2872340341c6b576a11d52a0b867fdbcd04389b4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723014"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>手順 1:サーバー プログラムを指定する (RDS チュートリアル)
最も一般的なケースとして、RDS を使用し[ます。](../../reference/rds-api/dataspace-object-rds.md)既定のサーバープログラム、 [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)、または独自のカスタムサーバープログラム (business オブジェクト) を指定するための、ユーザースペースオブジェクトの[CreateObject](../../reference/rds-api/createobject-method-rds.md)メソッド。 サーバープログラムはサーバー上でインスタンス化され、サーバープログラム ( *プロキシ*) への参照が返されます。  
  
 このチュートリアルでは、既定のサーバープログラムを使用します。  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="see-also"></a>参照  
 [手順 2: サーバープログラムを起動する (RDS チュートリアル)](./step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)