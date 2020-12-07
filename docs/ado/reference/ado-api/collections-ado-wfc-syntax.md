---
description: Collections (ADO - WFC 構文)
title: Collections (ADO-WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
author: rothja
ms.author: jroth
ms.openlocfilehash: a6afa603b169949673544791849ecbbc5d312cfb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975343"
---
# <a name="collections-ado---wfc-syntax"></a>Collections (ADO - WFC 構文)
**パッケージ com.. wfc. データ**  
  
## <a name="parameters"></a>パラメーター  
  
### <a name="methods"></a>メソッド  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>フィールド  
  
### <a name="methods"></a>メソッド  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>エラー  
  
### <a name="methods"></a>メソッド  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>参照  
 [Errors コレクション (ADO)](./errors-collection-ado.md)   
 [Fields コレクション (ADO)](./fields-collection-ado.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)