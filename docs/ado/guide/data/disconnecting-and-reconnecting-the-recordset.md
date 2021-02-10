---
description: レコードセットの切断と再接続
title: レコードセットの切断と再接続 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: rothja
ms.author: jroth
ms.openlocfilehash: dacaeae0406e42bb39c7fb7836aab20ff2bc1ad5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033242"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>レコードセットの切断と再接続
ADO で最も強力な機能の1つとして、データソースからクライアント側のレコードセットを開き、データソースからレコードセットを切断する機能があります。 レコードセットが切断されると、データソースへの接続を閉じることができます。これにより、管理に使用されたサーバー上のリソースが解放されます。 接続が切断された状態で、レコードセット内のデータを引き続き表示および編集し、後でデータソースに再接続して更新をバッチモードで送信することができます。  
  
 レコードセットを切断するには、カーソル位置を adUseClient にして開き、[ActiveConnection] プロパティを [なし] に設定します。 (C++ ユーザーは、ActiveConnection を NULL に設定して切断する必要があります)。  
  
 このセクションの後半では、切断されたレコードセットを使用します。このシナリオでは、レコードセットの永続化について説明し、クライアントコンピューターがネットワークに接続されていない状態で、レコードセット内のデータをアプリケーションで使用できるようにする必要があるシナリオに対処します。  
  
## <a name="see-also"></a>参照  
 [バッチ モード](./batch-mode.md)