---
description: ADOX の列挙定数
title: ADOX 列挙定数 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f9734a802ca1b653a912a0fe829b24e14e6953f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99164344"
---
# <a name="adox-enumerated-constants"></a>ADOX の列挙定数
デバッグを支援するために、ADOX 列挙定数は各定数の値を一覧表示します。 ただし、この値は純粋にアドバイザリであり、ADOX のあるリリースから別のリリースに変更される可能性があります。 コードは、列挙定数の実際の値ではなく、名前のみに依存する必要があります。  
  
 次の列挙定数が定義されています。  
  
|列挙|説明|  
|-----------------|-----------------|  
|[ActionEnum](./actionenum.md)|**SetPermissions** が呼び出されたときに実行されるアクションの種類を指定します。|  
|[AllowNullsEnum](./allownullsenum.md)|Null 値を持つレコードのインデックスを作成するかどうかを指定します。|  
|[ColumnAttributesEnum](./columnattributesenum.md)|**列** の特性を指定します。|  
|[DataTypeEnum](../ado-api/datatypeenum.md)|**フィールド**、**パラメーター**、または **プロパティ** のデータ型を指定します。|  
|[InheritTypeEnum](./inherittypeenum.md)|**SetPermissions** で設定された権限をオブジェクトが継承する方法を指定します。|  
|[KeyTypeEnum](./keytypeenum.md)|**キー** の種類 (プライマリ、外部、または一意) を指定します。|  
|[ObjectTypeEnum](./objecttypeenum.md)|権限または所有権を設定するデータベースオブジェクトの種類を指定します。|  
|[RightsEnum](./rightsenum.md)|オブジェクトのグループまたはユーザーの権限または権限を指定します。|  
|[RuleEnum](./ruleenum.md)|**キー** が削除されたときに従うルールを指定します。|  
|[SortOrderEnum](./sortorderenum.md)|インデックス付き列の並べ替え順序を指定します。|  
  
## <a name="see-also"></a>参照  
 [ADOX API リファレンス](./adox-object-model.md)   
 [データ定義言語とセキュリティの ADO 拡張機能 (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)