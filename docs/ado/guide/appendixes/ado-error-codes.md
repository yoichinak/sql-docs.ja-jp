---
description: ADO エラーコードのキャプチャ
title: ADO エラーコード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d3b0fd0c3a673cc841d7a5318872151bc20b311
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100029506"
---
# <a name="capture-ado-error-codes"></a>ADO エラーコードのキャプチャ
ADO 自体は、 [errors](../../reference/ado-api/errors-collection-ado.md)コレクションの[Error](../../reference/ado-api/error-object.md)オブジェクトで返されるプロバイダーエラーに加えて、実行時環境の例外処理機構にエラーを返すことができます。 ADO エラーをキャプチャするには、Microsoft® Visual Basic の **On error** ステートメントや Microsoft Visual C++®の **try-catch** ブロックなどのプログラミング言語を使用します。

 ADO エラーコードの一覧については、「 [Errorvalueenum](../../reference/ado-api/errorvalueenum.md)」を参照してください。

## <a name="see-also"></a>参照
 [エラーオブジェクト](../../reference/ado-api/error-object.md)[エラーの収集 (ADO)](../../reference/ado-api/errors-collection-ado.md)