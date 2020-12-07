---
description: ADOX オブジェクト
title: ADOX Objects |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: c38b184164109ee3e6fed18a439cd904119a3ec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985663"
---
# <a name="adox-objects"></a>ADOX オブジェクト
## <a name="adox-object-summary"></a>ADOX オブジェクトの概要  
  
|Object|説明|  
|------------|-----------------|  
|[カタログ](./catalog-object-adox.md)|データソースのスキーマカタログを記述するコレクションが含まれます。|  
|[列](./column-object-adox.md)|テーブル、インデックス、またはキーからの列を表します。|  
|[グループ](./group-object-adox.md)|セキュリティで保護されたデータベース内でアクセス許可を持つグループアカウントを表します。|  
|[Index](./index-object-adox.md)|データベーステーブルのインデックスを表します。|  
|[キー](./key-object-adox.md)|データベーステーブルの主キー、外部キー、または一意キーフィールドを表します。|  
|[手順](./procedure-object-adox.md)|ストアドプロシージャを表します。|  
|[Table](./table-object-adox.md)|列、インデックス、およびキーを含むデータベーステーブルを表します。|  
|[ユーザー](./user-object-adox.md)|セキュリティで保護されたデータベース内でアクセス許可を持つユーザーアカウントを表します。|  
|[表示](./view-object-adox.md)|フィルター処理されたレコードセットまたは仮想テーブルを表します。|  
  
 これらのオブジェクト間のリレーションシップは、 [ADOX オブジェクトモデル](./adox-object-model.md)で示されています。  
  
 各オブジェクトは、対応するコレクションに含めることができます。 たとえば、 **テーブル** オブジェクトを [Tables](./tables-collection-adox.md) コレクションに含めることができます。 詳細については、「 [ADOX Collections](./adox-collections.md) 」または「特定のコレクション」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ADOX API リファレンス](./adox-object-model.md?view=sql-server-ver15)   
 [ADOX コレクション](./adox-collections.md)   
 [ADOX オブジェクトモデル](./adox-object-model.md)   
 [データ定義言語とセキュリティの ADO 拡張機能 (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)