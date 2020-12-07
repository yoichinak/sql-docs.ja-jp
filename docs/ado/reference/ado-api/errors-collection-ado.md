---
description: Errors コレクション (ADO)
title: Errors コレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: rothja
ms.author: jroth
ms.openlocfilehash: 3606827f95330bf75915463bba8225bccdc62cd7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973623"
---
# <a name="errors-collection-ado"></a>Errors コレクション (ADO)
プロバイダーに関連する単一のエラーへの応答として作成されたすべての [エラー](../../../ado/reference/ado-api/error-object.md) オブジェクトが含まれます。  
  
## <a name="remarks"></a>解説  
 ADO オブジェクトに関連する操作では、1つ以上のプロバイダーエラーが発生することがあります。 各エラーが発生すると、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの**エラー**コレクションに1つまたは複数の**エラー**オブジェクトを配置できます。 別の ADO 操作によっ**てエラーが**生成されると、 **errors**コレクションがクリアされ、エラーオブジェクトの新しいセットを**errors**コレクションに配置できます。  
  
 各 **Error** オブジェクトは、ADO エラーではなく、特定のプロバイダーエラーを表します。 ADO エラーは、ランタイム例外処理機構に公開されます。 たとえば、Microsoft Visual Basic で ADO 固有のエラーが発生すると、 [onError](../../../ado/reference/rds-api/onerror-event-rds.md) イベントがトリガーされ、 **Err** オブジェクトに表示されます。  
  
 エラーを生成しない ADO 操作は、 **Errors** コレクションには影響しません。 **エラー**コレクションを手動で消去するには、 [clear](../../../ado/reference/ado-api/clear-method-ado.md)メソッドを使用します。  
  
 **Errors**コレクション内の**エラー**オブジェクトのセットには、1つのステートメントに応答して発生したすべてのエラーが記述されています。 **Errors**コレクションの特定のエラーを列挙すると、エラー処理ルーチンは、エラーの原因と原因をより正確に特定し、回復するための適切な手順を実行できます。  
  
 一部のプロパティおよびメソッドは、**エラーコレクションに****エラー**オブジェクトとして表示されるが、プログラムの実行を停止しない警告を返します。 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド、 **Connection**オブジェクトの[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッド、または**recordset**オブジェクトの[Filter](../../../ado/reference/ado-api/filter-property.md)プロパティの設定を呼び出す前に、 **Errors**コレクションに対して**Clear**メソッドを呼び出します。 これにより、 **Errors**コレクションの[Count](../../../ado/reference/ado-api/count-property-ado.md)プロパティを読み取って、返された警告をテストできます。  
  
> [!NOTE]
>  1つの ADO 操作で複数のエラーを生成する方法の詳細については、 **Error** オブジェクトのトピックを参照してください。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Errors コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
