---
description: 一意のテーブル、一意のスキーマ、一意のカタログ Properties-Dynamic (ADO)
title: レコードセットベーステーブルへの変更の制御 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: rothja
ms.author: jroth
ms.openlocfilehash: 485fe00e6f55e6916341fd4420f0aaaa395fe54b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170049"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>一意のテーブル、一意のスキーマ、一意のカタログ Properties-Dynamic (ADO)
複数のベーステーブルに対する結合操作によって形成された [レコードセット](./recordset-object-ado.md) 内の特定のベーステーブルに対する変更を厳密に制御できます。  
  
-   **一意のテーブル** 更新、挿入、および削除が許可されるベーステーブルの名前を指定します。  
  
-   [**一意のスキーマ**]*スキーマ* またはテーブルの所有者の名前を指定します。  
  
-   **一意のカタログ***カタログ* を指定します。または、テーブルを含むデータベースの名前を指定します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 テーブル、スキーマ、またはカタログの名前を示す **文字列** 値を設定または返します。  
  
## <a name="remarks"></a>コメント  
 目的のベーステーブルは、そのカタログ名、スキーマ名、およびテーブル名によって一意に識別されます。 一意の **テーブル** プロパティが設定されている場合は、 **一意のスキーマ** または一意の **カタログ** プロパティの値を使用してベーステーブルが検索されます。 一意の **テーブル** プロパティが設定される前に、一意の **スキーマ** と **一意のカタログ** プロパティのどちらかまたは両方が設定されていることを前提としていますが、必須ではありません。  
  
 **一意のテーブル** の主キーは、**レコードセット** 全体の主キーとして扱われます。 これは、主キーを必要とする任意のメソッドに使用されるキーです。  
  
 **一意のテーブル** が設定されている間、 [Delete](./delete-method-ado-recordset.md)メソッドは、指定されたテーブルのみに影響します。 [AddNew](./addnew-method-ado.md)、 [Resync](./resync-method.md)、 [Update](./update-method.md)、および [UpdateBatch](./updatebatch-method.md)の各メソッドは、**レコードセット** の基になるベーステーブルに影響します。  
  
 カスタムの再同期を実行する前に、**一意のテーブル** を指定する必要があります。 **一意のテーブル** が指定されていない場合、再 [同期コマンド](./resync-command-property-dynamic-ado.md)のプロパティは無効になります。  
  
 一意のベーステーブルが見つからない場合、実行時エラーが発生します。  
  
 [カーソル位置](./cursorlocation-property-ado.md)プロパティが **adUseClient** に設定されている場合、これらの動的プロパティはすべて、**レコードセット** オブジェクトの [プロパティ](./properties-collection-ado.md)コレクションに追加されます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)