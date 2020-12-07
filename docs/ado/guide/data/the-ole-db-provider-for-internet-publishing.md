---
description: OLE DB Provider for Internet Publishing
title: OLE DB Provider for Internet Publishing |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: rothja
ms.author: jroth
ms.openlocfilehash: 7556d3857142a4762fd411f5175a38c2e4d58cf3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979363"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>OLE DB Provider for Internet Publishing
ADO [レコード](../../../ado/reference/ado-api/record-object-ado.md) および [ストリーム](../../../ado/reference/ado-api/stream-object-ado.md) オブジェクトは、Microsoft OLE DB Provider For Internet Publishing (internet publishing provider) と共に使用して、microsoft FrontPage によって提供される Web フォルダーやファイルなどのリソースにアクセスしたり操作したりすることができます。 ADO では、 **レコード**、 **ストリーム**、または [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md) のソースを URL に指定できます。 その後、リソースのアップロード、ダウンロード、移動、コピー、削除、またはリソースプロパティの直接操作を行うことができます。  
  
 インターネット発行プロバイダーで **レコード** と **ストリーム** を使用するコード例については、「 [インターネット発行のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)」を参照してください。  
  
 インターネット公開プロバイダーは、Microsoft Windows 2000 と共にインストールされます。 以前のバージョンのインターネット発行プロバイダーは、Microsoft Office 2000 および Microsoft Internet Explorer 5.0 でも使用できます。  
  
 ADO をインターネット発行プロバイダーに接続するには、次の3つの方法があります。  
  
-   接続文字列に "URL =" を指定します。 次に例を示します。  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   接続文字列の *Provider* キーワードに対して、Msdaipp を指定します。 次に例を示します。  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   [接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティには、Msdaipp を指定します。 次に例を示します。  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  *プロバイダーの接続文字列*キーワードまたは**プロバイダー**プロパティを使用して、プロバイダーの値として Msdaipp が明示的に指定されている場合、接続文字列で "URL =" を使用することはできません。 そうすると、エラーが発生します。 代わりに、前述のように URL を指定するだけです。  
  
 インターネット公開プロバイダーの詳細については、「 [Microsoft OLE DB provider For Internet publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)」または「インターネット発行用の OLE DB プロバイダーがインストールされているソースアプリケーションに付属のプロバイダードキュメント (Windows 2000、Office 2000、または internet Explorer 5.0)」を参照してください。
