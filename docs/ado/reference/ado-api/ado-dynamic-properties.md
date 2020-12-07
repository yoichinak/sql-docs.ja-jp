---
description: ADO の動的プロパティ
title: ADO 動的プロパティ |Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd0186fba696d2fe3528f113bd0e07aeadd801f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976513"
---
# <a name="ado-dynamic-properties"></a>ADO の動的プロパティ
動的プロパティは、[接続](./connection-object-ado.md)、[コマンド](./command-object-ado.md)、または[レコードセット](./recordset-object-ado.md)オブジェクトの[properties](./properties-collection-ado.md)コレクションに追加できます。 これらのプロパティのソースは、データプロバイダー ( [SQL Server の OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)、 [OLE DB 用の Microsoft Cursor service](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)などのサービスプロバイダー) のいずれかです。 特定の動的プロパティの詳細については、適切なデータプロバイダーまたはサービスプロバイダーのドキュメントを参照してください。  
  
 [Ado 動的プロパティインデックス](./ado-dynamic-property-index.md)は、各標準 OLE DB プロバイダー動的プロパティの ado と OLE DB 名の間の相互参照を提供します。  
  
 次の動的プロパティは特に興味深いものであり、前述のソースにも記載されています。 ADO を使用した特殊な機能については、次の一覧の ADO ヘルプトピックを参照してください。  
  
|動的プロパティ|説明|  
|-|-|  
|[最適化](./optimize-property-dynamic-ado.md)|このフィールドにインデックスを作成するかどうかを指定します。|  
|[プロンプト](./prompt-property-dynamic-ado.md)|OLE DB プロバイダーがユーザーに初期化情報の入力を求めるかどうかを指定します。|  
|[名前のリシェイプ](./reshape-name-property-dynamic-ado.md)|**レコードセット**オブジェクトの名前を指定します。|  
|[再同期コマンド](./resync-command-property-dynamic-ado.md)|**一意のテーブル**動的プロパティに指定されたテーブル内のデータを更新するために再**同期**メソッドによって発行される、ユーザーが指定したコマンド文字列を指定します。|  
|[一意のテーブル、一意のスキーマ、一意のカタログ](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**一意のテーブル** 更新、挿入、および削除が許可されるベーステーブルの名前を指定します。<br /><br /> **一意のスキーマ** スキーマ、またはテーブルの所有者の名前を指定します。<br /><br /> **一意のカタログ** カタログ、またはテーブルを含むデータベースの名前を指定します。|  
|[再同期の更新](./update-resync-property-dynamic-ado.md)|**UpdateBatch**メソッドの後に暗黙の再**同期**メソッド操作を実行するかどうかを指定します。それを行う場合は、その操作のスコープを指定します。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO 列挙定数](./ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](./ado-events.md)   
 [ADO メソッド](./ado-methods.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](./ado-objects-and-interfaces.md)   
 [ADO のプロパティ](./ado-properties.md)