---
description: 'コレクション (Visual C++ 構文インデックス #import)'
title: 'コレクション (Visual C++ 構文インデックス #import) |Microsoft Docs'
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
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e29b092ea7c11dc9729986c342c96b2022fbf58
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99164673"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>コレクション (Visual C++ 構文インデックス #import)
コレクションが特定の共通メソッドとプロパティを継承することを理解しておくと便利です。  
  
 すべてのコレクションは **Count** プロパティと **Refresh** メソッドを継承し、すべてのコレクションが **Item** プロパティを追加します。 **Errors** コレクションは **Clear** メソッドを追加します。 **Parameters** コレクションは、 **Append** メソッドと **delete** メソッドを継承しますが、Fields コレクションは、 **Append**、 **delete**、および **Update** の **各** メソッドを追加します。  
  
## <a name="properties-collection"></a>プロパティのコレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>Errors コレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters コレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Fields コレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>参照  
 [Errors コレクション (ADO)](./errors-collection-ado.md)   
 [Fields コレクション (ADO)](./fields-collection-ado.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)