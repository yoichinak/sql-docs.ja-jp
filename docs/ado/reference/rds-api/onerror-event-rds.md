---
description: onError イベント (RDS)
title: onError イベント (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: rothja
ms.author: jroth
ms.openlocfilehash: 56caf584d45b76315ff95cf6001a2ce1c882f579
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724463"
---
# <a name="onerror-event-rds"></a>onError イベント (RDS)
**OnError**イベントは、操作中にエラーが発生するたびに呼び出されます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>パラメーター  
 *SCode*  
 エラーのステータスコードを示す整数。  
  
 *説明*  
 エラーの説明を示す **文字列** 。  
  
 *ソース*  
 エラーの原因となったクエリまたはコマンドを示す **文字列** 。  
  
 *CancelDisplay*  
 **ブール**値。 **True**に設定すると、ダイアログボックスにエラーが表示されなくなります。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](../ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../guide/data/ado-event-handler-summary.md)