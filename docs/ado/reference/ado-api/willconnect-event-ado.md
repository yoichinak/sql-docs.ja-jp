---
description: WillConnect イベント (ADO)
title: 接続イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 259ef55060d7968d9ec557c831412ad58609a6df
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987783"
---
# <a name="willconnect-event-ado"></a>WillConnect イベント (ADO)
接続が開始 **される前に、イベントが** 呼び出されます。  
  
 **適用対象:** [接続オブジェクト (ADO)](./connection-object-ado.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *文字列*  
 保留中の接続の接続情報を含む **文字列** 。  
  
 *UserID*  
 保留中の接続のユーザー名を含む **文字列** 。  
  
 *パスワード*  
 保留中の接続のパスワードを含む **文字列** 。  
  
 *Options*  
 プロバイダーが*ConnectionString*を評価する方法を示す**Long 型**の値。 唯一のオプションは **adAsyncOpen**です。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。  
  
 このイベントが呼び出されると、このパラメーターは既定で **Adstatusok** に設定されます。 イベントが保留中の操作の取り消しを要求できない場合は、 **Adstatuscantdeny** に設定されます。  
  
 このイベントが返される前に、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。 このパラメーターを **Adstatuscancel** に設定して、この通知の取り消しの原因となった接続操作を要求します。  
  
 *pConnection*  
 このイベント通知を適用する [接続](./connection-object-ado.md) オブジェクト。 に**よって接続の**パラメーターを**変更して****も、接続**に影響はありません。  
  
## <a name="remarks"></a>解説  
 を **呼び出すと、** *ConnectionString*、 *UserID*、 *Password*、および *Options* の各パラメーターは、このイベントの原因となった操作によって確立された値 (保留中の接続) に設定され、イベントが返される前に変更できます。 **接続** によって、保留中の接続が取り消されたという要求が返される場合があります。  
  
 このイベントがキャンセルされると、 **Connectcomplete** が呼び出され、 *Adstatus* パラメーターが **Adstatuserrorの curred**に設定されます。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../guide/data/ado-event-handler-summary.md)