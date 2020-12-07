---
description: InternetTimeout プロパティ (RDS)
title: InternetTimeout プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: rothja
ms.author: jroth
ms.openlocfilehash: 43ab46eefcb897511a2990655362ecb10527be19
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724503"
---
# <a name="internettimeout-property-rds"></a>InternetTimeout プロパティ (RDS)
要求がタイムアウトするまでのミリ秒単位の待機時間を示します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 要求がタイムアウトするまでのミリ秒数を表す **Long 型** の値を設定または返します。  
  
## <a name="remarks"></a>解説  
 このプロパティは、HTTP または HTTPS プロトコルを使用して送信された要求にのみ適用されます。  
  
 3層環境での要求の実行には数分かかる場合があります。 このプロパティを使用して、長時間実行される要求に追加の時間を指定します。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataSpace オブジェクト (RDS)](./dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [InternetTimeout プロパティの例 (VB)](./internettimeout-property-example-vb.md)   
 [InternetTimeout プロパティの例 (VC++)](./internettimeout-property-example-vc.md)