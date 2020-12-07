---
description: 階層レコードセットの保持
title: 階層レコードセットの保持 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: rothja
ms.author: jroth
ms.openlocfilehash: b3764011c0ce0e3a49a17b20cbb344b5e98218d7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724953"
---
# <a name="persisting-hierarchical-recordsets"></a>階層レコードセットの保持
ADTG 形式または XML 形式のファイルに階層 **レコードセット** を保存するには、 [save](../../../ado/reference/ado-api/save-method.md) メソッドを呼び出します。 ただし、階層 **レコード**セットを xml 形式で保存する場合は、2つの制限があります。階層 **レコードセット** に保留中の更新が含まれている場合は xml で保存できません。また、パラメーター化された階層 **レコードセット**を保存することもできません。  
  
 データシェイププロバイダーの詳細については、「 [Microsoft data](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) OLE DB for OLE DB (ADO)」および「 [データシェイプサービスの概要](/previous-versions/windows/desktop/ms719615(v=vs.85))」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [仮形の文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)