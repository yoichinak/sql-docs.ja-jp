---
description: DataControl オブジェクトのエラーコード
title: DataControl のエラーコード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
author: rothja
ms.author: jroth
ms.openlocfilehash: 3554898451228afee73914a82907f6348ad1cff0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991133"
---
# <a name="datacontrol-object-error-codes"></a>DataControl オブジェクトのエラーコード
次の表に、RDS の一覧を示し [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクトのエラーコード。 小さい2バイトの正の10進変換、完全なエラーコードの負の10進変換、および16進数の値が表示されます。

|RDS.DataControl エラーコード|Number|説明|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|非同期操作が保留中であるため、操作を実行できません。|
|**IDS_BadInlineTablegram**|4105-2146824183 0x800A1009|インライン tablegram が正しくありません。|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|サーバーに接続できません。|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|ビジネスオブジェクトを作成できません。|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|値スペースプロパティが無効です。|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|ビジネスオブジェクトでメソッドを呼び出すことはできません。|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|このページでは、別のドメインのデータにアクセスします。 これを許可しますか? Internet Explorer でこのメッセージを表示しないようにするには、[**インターネットオプション**] ダイアログボックスの [**セキュリティ**] タブで、信頼済みサイトゾーンにセキュリティで保護された Web サイトを追加します。|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|無効な RDS クライアントバージョンです-クライアントはサーバーよりも新しいバージョンです。|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|1 つ以上の引数が無効です。|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|バインドプロパティにエラーがあります。|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|1 つ以上の引数が無効です。|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|そのようなインターフェイスはサポートされていません。|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|イベントハンドラーがまだ処理中であるため、要求を実行できません。|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|このコンピューターの安全性の設定により、ビジネスオブジェクトの作成が禁止されています。|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|**レコードセット** が開かれていません。|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|**Sortcolumn**または**filtercolumn**に指定された列が存在しません。|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|行セットは更新できません。|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|予期しないエラー。|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|データベースを更新できません。|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|DataControl **URL** プロパティには Urlmon.dll システムファイルが必要ですが、見つかりません。|

## <a name="see-also"></a>参照
 [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)