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
ms.openlocfilehash: aa933f7be33f564af3aaf2851f6ec32bd5b4c5d4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991183"
---
# <a name="capture-ado-error-codes"></a>ADO エラーコードのキャプチャ
ADO 自体は、 [errors](../../reference/ado-api/errors-collection-ado.md)コレクションの[Error](../../reference/ado-api/error-object.md)オブジェクトで返されるプロバイダーエラーに加えて、実行時環境の例外処理機構にエラーを返すことができます。 ADO エラーをキャプチャするには、Microsoft® Visual Basic の **On error** ステートメントや Microsoft Visual C++®の **try-catch** ブロックなどのプログラミング言語を使用します。

 ADO エラーコードの一覧については、「 [Errorvalueenum](../../reference/ado-api/errorvalueenum.md)」を参照してください。

## <a name="see-also"></a>参照
 [エラーオブジェクト](../../reference/ado-api/error-object.md)[エラーの収集 (ADO)](../../reference/ado-api/errors-collection-ado.md)