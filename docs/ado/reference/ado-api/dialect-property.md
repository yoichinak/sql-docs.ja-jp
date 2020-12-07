---
description: Dialect プロパティ
title: Dialect プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: rothja
ms.author: jroth
ms.openlocfilehash: be93ceb76aa0aadba5b28673c16704b0881186f9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973903"
---
# <a name="dialect-property"></a>Dialect プロパティ
[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)または[commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティの言語を示します。 この言語では、文字列またはストリームを解析するためにプロバイダーが使用する構文と一般規則が定義されています。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **Dialect**プロパティには、コマンドテキストまたはストリームの言語を表す有効な GUID が含まれています。 このプロパティの既定値は {C8B521FB-5CF3-11CE-ADE5-00AA0044773D} です。これは、プロバイダーがコマンドテキストまたはストリームを解釈する方法を選択する必要があることを示します。  
  
## <a name="remarks"></a>解説  
 ADO は、ユーザーがこのプロパティの値を読み取ったときにプロバイダーに対してクエリを実行しません。このメソッドは、現在 [Command](../../../ado/reference/ado-api/command-object-ado.md) オブジェクトに格納されている値の文字列形式を返します。  
  
 ユーザーが **Dialect** プロパティを設定すると、ADO によって guid が検証され、指定した値が有効な guid でない場合はエラーが発生します。 **Dialect**プロパティでサポートされている GUID 値を確認するには、プロバイダーのドキュメントを参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Execute メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)
