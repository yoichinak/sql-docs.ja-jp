---
description: Collections (Visual C++ 構文用の ADO)
title: Collections (Visual C++ 構文用の ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cda61fc0d1d206a75059263c5450c813a9e5ddb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99164692"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Collections (Visual C++ 構文用の ADO)
## <a name="parameters"></a>パラメーター  
  
### <a name="methods"></a>メソッド  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Append メソッド (ADO)](./append-method-ado.md)  
  
-   [Delete メソッド (ADO Parameters コレクション)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh メソッド (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](./count-property-ado.md)  
  
-   [Item プロパティ (ADO)](./item-property-ado.md)  
  
## <a name="fields"></a>フィールド  
  
### <a name="methods"></a>メソッド  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Append メソッド (ADO)](./append-method-ado.md)  
  
-   [Delete メソッド (ADO Parameters コレクション)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh メソッド (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](./count-property-ado.md)  
  
-   [Item プロパティ (ADO)](./item-property-ado.md)  
  
## <a name="errors"></a>エラー  
  
### <a name="methods"></a>メソッド  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Clear メソッド (ADO)](./clear-method-ado.md)  
  
-   [Refresh メソッド (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](./count-property-ado.md)  
  
-   [Item プロパティ (ADO)](./item-property-ado.md)  
  
## <a name="properties"></a>Properties  
  
### <a name="methods"></a>メソッド  
  
```  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Refresh メソッド (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](./count-property-ado.md)  
  
-   [Item プロパティ (ADO)](./item-property-ado.md)  
  
## <a name="see-also"></a>参照  
 [Errors コレクション (ADO)](./errors-collection-ado.md)   
 [Fields コレクション (ADO)](./fields-collection-ado.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)