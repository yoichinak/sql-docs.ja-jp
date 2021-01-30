---
description: Append メソッド (ADOX Columns)
title: Append メソッド (ADOX Columns) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 40abf0ae298b469d0814e8dd3da85a8c8865be78
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169596"
---
# <a name="append-method-adox-columns"></a>Append メソッド (ADOX Columns)
[Columns](./columns-collection-adox.md)コレクションに新しい[Column](./column-object-adox.md)オブジェクトを追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *列*  
 追加する **列** オブジェクト、または作成して追加する列の名前。  
  
 *Type*  
 任意。 列のデータ型を指定する **Long** 型の値です。 *Type* パラメーターは、 **Column** オブジェクトの [type](./type-property-column-adox.md)プロパティに対応しています。  
  
 *DefinedSize*  
 任意。 列のサイズを指定する **Long 型** の値です。 指定された *サイズ* のパラメーターは、 **Column** オブジェクトの "指定された [サイズ](./definedsize-property-adox.md)" プロパティに対応します。  
  
> [!NOTE]
>  [テーブル](./tables-collection-adox.md)コレクションに既に追加されている [テーブル](./table-object-adox.md)**に列が** 存在しない場合、[インデックス](./index-object-adox.md)の **Columns** コレクションに **列** を追加すると、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Columns コレクション (ADOX)](./columns-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)   
 [Append メソッド (ADOX Groups)](./append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](./append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](./append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)