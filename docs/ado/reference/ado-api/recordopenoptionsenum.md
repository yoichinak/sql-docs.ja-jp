---
description: RecordOpenOptionsEnum
title: RecordOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: rothja
ms.author: jroth
ms.openlocfilehash: 352622f55e82b1941439a242249e067aae090e51
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989783"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
[レコード](./record-object-ado.md)を開くためのオプションを指定します。 これらの値は、またはを使用して組み合わせることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|**レコード**に関連付けられているフィールドを最初に取得する必要がないことをプロバイダーに示しますが、最初にフィールドにアクセスしようとしたときに取得できます。 このフラグを指定しないと、既定の動作では、すべての **レコード** オブジェクトフィールドが取得されます。|  
|**adDelayFetchStream**|0x4000|**レコード**に関連付けられた既定のストリームを最初に取得する必要がないことをプロバイダーに示します。 既定の動作では、このフラグが指定されていない場合に、 **Record** オブジェクトに関連付けられている既定のストリームを取得します。|  
|**adOpenAsync**|0x1000|**レコード**オブジェクトが非同期モードで開かれていることを示します。|  
|**adOpenExecuteCommand**|0x10000|実行する必要のあるコマンドテキストがソース文字列に含まれていることを示します。 この値は、**レコードセット**の**adcmdtext**オプションに相当します。 Open.|  
|**adOpenRecordUnspecified**|-1|既定値。 オプションが指定されていないことを示します。|  
|**adOpenOutput 出力**|0x800000|ソースが実行可能スクリプト (など) を含むノードを参照している場合に、これを示します。ASP ページ)、開いている **レコード** には、実行したスクリプトの結果が含まれます。 この値は、非コレクションレコードでのみ有効です。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Record)](./open-method-ado-record.md)