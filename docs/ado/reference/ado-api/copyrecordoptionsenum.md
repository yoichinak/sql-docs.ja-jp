---
description: CopyRecordOptionsEnum
title: CopyRecordOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: rothja
ms.author: jroth
ms.openlocfilehash: 2afe394c4b6251ea21d7245d55ab905ba6347fcc
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167683"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
[Copyrecord](./copyrecord-method-ado.md)メソッドの動作を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|*ターゲット* が別のサーバー上にあるか、*ソース* とは異なるプロバイダーによって処理されることが原因でこのメソッドが失敗した場合 *に、ダウンロード* およびアップロード操作を使用してコピーをシミュレートしようとすることを示します。 プロバイダーの機能が異なると、パフォーマンスが低下したり、データが失われることがあります。|  
|**adCopyNonRecursive**|2|現在のディレクトリをコピー先にコピーします。ただし、そのサブディレクトリはコピーしません。 コピー操作は再帰的ではありません。|  
|**adCopyOverWrite**|1|*コピー先* が既存のファイルまたはディレクトリを指している場合、ファイルまたはディレクトリを上書きします。|  
|**adCopyUnspecified**|-1|既定値。 既定のコピー操作を実行します。コピー先のファイルまたはディレクトリが既に存在し、操作が再帰的にコピーされる場合、操作は失敗します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [CopyRecord メソッド (ADO)](./copyrecord-method-ado.md)