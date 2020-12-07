---
description: Column オブジェクト (ADOX)
title: Column オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: rothja
ms.author: jroth
ms.openlocfilehash: b6cc15e82091da2161a01c1c0a468e86095dd0d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985103"
---
# <a name="column-object-adox"></a>Column オブジェクト (ADOX)
テーブル、インデックス、またはキーからの列を表します。  
  
## <a name="remarks"></a>解説  
 次のコードでは、新しい **列**を作成します。  
  
 `Dim obj As New Column`  
  
 **Column**オブジェクトのプロパティとコレクションを使用すると、次のことができます。  
  
-   [Name プロパティ (ADOX)](./name-property-adox.md)プロパティを使用して、列を特定します。  
  
-   [Type プロパティ (キー) (ADOX)](./type-property-key-adox.md)プロパティを使用して、列のデータ型を指定します。  
  
-   列が固定長であるかどうか、または [Attributes プロパティ (ADOX)](./attributes-property-adox.md) プロパティを使用して null 値を含むことができるかどうかを確認します。  
  
-   列の最大サイズを指定するには、"設定された [サイズ" プロパティ (ADOX)](./definedsize-property-adox.md) プロパティを使用します。  
  
-   数値データ値の場合は、 [Numericscale プロパティ (ADOX)](./numericscale-property-adox.md) プロパティを使用して小数点以下桁数を指定します。  
  
-   数値データ値については、 [Precision プロパティ (ADOX)](./precision-property-adox.md) プロパティを使用して最大有効桁数を指定します。  
  
-   [ParentCatalog property (adox)](./parentcatalog-property-adox.md)プロパティを使用して、列を所有する[カタログオブジェクト (adox)](./catalog-object-adox.md)を指定します。  
  
-   キー列の場合は、関連テーブル内の関連する列の名前を、"関連付け [列のプロパティ (ADOX)](./relatedcolumn-property-adox.md) " プロパティを使用して指定します。  
  
-   [インデックス列] では、並べ替え順序が並べ替え順序 [として](./sortorder-property-adox.md) 昇順と降順のどちらであるかを指定します。  
  
-   [プロパティコレクション (ADO)](../ado-api/properties-collection-ado.md)コレクションを使用して、プロバイダー固有のプロパティにアクセスします。  
  
> [!NOTE]
>  **列**オブジェクトのすべてのプロパティがデータプロバイダーでサポートされているとは限りません。 プロバイダーがサポートしていないプロパティの値を設定した場合、エラーが発生します。 新しい **列** オブジェクトの場合、オブジェクトがコレクションに追加されるとエラーが発生します。 既存のオブジェクトの場合、プロパティの設定時にエラーが発生します。  
>   
>  **列**オブジェクトを作成するときに、オプションのプロパティに適切な既定値が存在しても、プロバイダーがプロパティをサポートしているかどうかは保証されません。 プロバイダーがサポートしているプロパティの詳細については、プロバイダーのドキュメントを参照してください。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Column オブジェクトのプロパティ、メソッド、およびイベント](./column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX のコード例: NumericScale および Precision プロパティの例 (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)   
 [順序のプロパティの例 (VB)](./sortorder-property-example-vb.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)