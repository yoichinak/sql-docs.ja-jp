---
description: Append メソッド (ADOX Keys)
title: Append メソッド (ADOX Keys) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: rothja
ms.author: jroth
ms.openlocfilehash: 2531031808c16db4892fb0b759a8a8d819a2222d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985483"
---
# <a name="append-method-adox-keys"></a>Append メソッド (ADOX Keys)
新しい [キー](./key-object-adox.md) オブジェクトを [Keys](./keys-collection-adox.md) コレクションに追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *キー*  
 追加する **キー** オブジェクト、または作成および追加するキーの名前。  
  
 *KeyType*  
 省略可能。 キーの種類を指定する **Long** 型の値です。 *キー*パラメーターは、**キー**オブジェクトの[Type](./type-property-key-adox.md)プロパティに対応します。  
  
 *列*  
 省略可能。 インデックスを作成する列の名前を指定する **文字列** 値。 *Columns*パラメーターは、 [Column](./column-object-adox.md)オブジェクトの[Name](./name-property-adox.md)プロパティの値に対応しています。  
  
 *RelatedTable*  
 省略可能。 関連するテーブルの名前を示す **文字列** 値です。 関連性*テーブル*のパラメーターは、 [Table](./table-object-adox.md)オブジェクトの**Name**プロパティの値に対応しています。  
  
 *RelatedColumn*  
 省略可能。 外部キーに関連付けられている列の名前を示す **文字列** 値です。 [関連性のある*列*のパラメーターは、 [Column](./column-object-adox.md)オブジェクトの**Name**プロパティの値に対応します。  
  
## <a name="remarks"></a>解説  
 *Columns*パラメーターには、列名または列名の配列のいずれかを指定できます。  
  
## <a name="applies-to"></a>適用対象  
 [Keys コレクション (ADOX)](./keys-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](./append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](./append-method-adox-indexes.md)   
 [Append メソッド (ADOX Procedures)](./append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)