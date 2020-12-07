---
description: ErrorValueEnum
title: ErrorValueEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 48962e163804eaa779f82789082e5b8d493bc3cd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973583"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
ADO ランタイムエラーの種類を指定します。  
  
 エラー番号には、次の3つの形式があります。  
  
-   正の10進数-10 進数形式の完全な2バイト。 この数値は、[既定の Visual Basic エラーメッセージ] ダイアログボックスに表示されます。 たとえば、実行時エラー ' 3707 ' です。  
  
-   負の decimal-完全なエラー番号の10進変換。  
  
-   16進数-完全なエラー番号の16進数表現。 Windows のファシリティコードは、4番目の数字です。 ADO エラー番号のファシリティ *コードはです。* 例: 0x800***A***0e7b。  
  
> [!NOTE]
>  ADO アプリケーションに OLE DB エラーが渡される場合があります。 通常、これらは Windows ファシリティコード *4*で識別できます。 たとえば、0x800***4***のようになります。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|Source として**Command**オブジェクトを含む**Recordset**オブジェクトの**ActiveConnection**プロパティを変更することはできません。|  
|**adErrCannotComplete**|3732-2146824556 0x800A0E94|サーバーは操作を完了できません。|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|接続が拒否されました。 要求された新しい接続は、既に使用されているものとは異なる特性を持っています。|  
|**adErrCantChangeProvider**|3220-2146825068 0X800A0C94|指定されたプロバイダーは、既に使用されているものと異なります。|  
|**adErrCantConvertvalue**|3724-2146824564 0x800A0E8C|符号の不一致またはデータのオーバーフロー以外の理由により、データ値を変換できません。 たとえば、変換によってデータが切り捨てられる場合があります。|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|フィールドのデータ型が不明であるか、プロバイダーの操作に必要なリソースが不足しているため、データ値を設定または取得できません。|  
|**adErrCatalogNotSet**|3747-2146824541 0x800A0EA3|操作には有効な **ParentCatalog**が必要です。|  
|**Aderrcolumnnotonこの行**|3726-2146824562 0x800A0E8E|レコードにこのフィールドが含まれていません。|  
|**adErrDataConversion**|3421-2146824867 0x800A0D5D|アプリケーションで、現在の操作に対して間違った型の値が使用されています。|  
|**adErrDataOverflow**|3721-2146824567 0x800A0E89|データ値が大きすぎて、フィールドのデータ型で表すことができません。|  
|**adErrDelResOutOfScope**|3738-2146824550 0x800A0E9A|削除するオブジェクトの URL が現在のレコードのスコープ外です。|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|プロバイダーは共有制限をサポートしていません。|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|プロバイダーは、要求された種類の共有制限をサポートしていません。|  
|**adErrFeatureNotAvailable**|3251-2146825037 0x800A0CB3|オブジェクトまたはプロバイダーが要求された操作を実行できません。|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|フィールドを更新できませんでした。 詳細については、個々のフィールドオブジェクトの **Status** プロパティを確認してください。|  
|**adErrIllegalOperation**|3219-2146825069 0x800A0C93|操作はこのコンテキストでは許可されていません。|  
|**adErrIntegrityViolation**|3719-2146824569 0x800A0E87|データ値がフィールドの整合性制約と競合しています。|  
|**adErrInTransaction**|3246-2146825042 0x800A0CAE|トランザクションでは、**接続**オブジェクトを明示的に閉じることができません。|  
|**adErrInvalidArgument**|3001-2146825287 0x800A0BB9|引数の型が正しくないか、許容範囲外であるか、または競合しています。|  
|**adErrInvalidConnection**|3709-2146824579 0x800A0E7D|この接続を使用してこの操作を実行することはできません。 このコンテキストでは、閉じられているか、無効です。|  
|**adErrInvalidParamInfo**|3708-2146824580 0x800A0E7C|**パラメーター** オブジェクトが正しく定義されていません。 一貫性のない情報または不完全な情報が提供されました。|  
|**adErrInvalidTransaction**|3714-2146824574 0x800A0E82|調整トランザクションが無効であるか、開始されていません。|  
|**adErrInvalidURL**|3729-2146824559 0x800A0E91|URL に無効な文字が含まれています。 URL が正しく入力されていることを確認します。|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|要求された名前または序数に対応する項目がコレクション内に見つかりません。|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|**BOF**または**EOF**が True であるか、または現在のレコードが削除されています。 要求された操作には現在のレコードが必要です。|  
|**adErrNotExecuting**|3715-2146824573 0x800A0E83|実行されていないときに操作を実行することはできません。|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|イベントの処理中に操作を実行することはできません。|  
|**adErrObjectClosed**|3704-2146824584 0x800A0E78|オブジェクトが閉じている場合、操作は許可されません。|  
|**adErrObjectInCollection**|3367-2146824921 0x800A0D27|オブジェクトは既にコレクションに含まれています。 を追加できません。|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|オブジェクトが有効ではなくなりました。|  
|**adErrObjectOpen**|3705-2146824583 0x800A0E79|オブジェクトが開いているときは、操作は許可されません。|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|ファイルを開けませんでした。|  
|**adErrOperationCancelled**|3712-2146824576 0x800A0E80|操作はユーザーによって取り消されました。|  
|**adErrOutOfSpace**|3734-2146824554 0x800A0E96|操作を実行できません。 プロバイダーが十分な記憶域スペースを取得できません。|  
|**adErrPermissionDenied**|3720-2146824568 0x800A0E88|権限が不十分なため、フィールドに書き込めません。|  
|**adErrProviderFailed**|3000-2146825288 0x800A0BB8|プロバイダーは要求された操作を実行しませんでした。|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|プロバイダーが見つかりません。 正しくインストールされていない可能性があります。|  
|**adErrReadFile**|3003-2146825285 0x800A0BBB|ファイルを読み取れませんでした。|  
|**adErrResourceExists**|3731-2146824557 0x800A0E93|コピー操作を実行できません。 送信先 URL で指定されたオブジェクトは既に存在します。 オブジェクトを置き換えるには、 **Adcopyoverwrite** を指定します。|  
|**adErrResourceLocked**|3730-2146824558 0x800A0E92|指定された URL によって表されるオブジェクトが、他の1つ以上のプロセスによってロックされています。 プロセスが終了するまで待ってから、操作を再試行してください。|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|送信元または送信先の URL が現在のレコードのスコープ外です。|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|データ値が、フィールドのデータ型または制約と競合しています。|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|データ値が符号付きで、プロバイダーで使用されるフィールドデータ型が符号なしであったため、変換できませんでした。|  
|**adErrStillConnecting**|3713-2146824575 0x800A0E81|非同期接続中に操作を実行することはできません。|  
|**adErrStillExecuting**|3711-2146824577 0x800A0E7F|非同期での実行中に操作を実行することはできません。|  
|**adErrTreePermissionDenied**|3728-2146824560 0x800A0E90|ツリーまたはサブツリーにアクセスするのに十分なアクセス許可がありません。|  
|**adErrUnavailable 不可**|3736-2146824552 0x800A0E98|操作が完了しませんでした。状態は使用できません。 フィールドが使用できないか、操作が試行されませんでした。|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|このコンピューターの安全性の設定により、別のドメインのデータソースにアクセスできません。|  
|**adErrURLDoesNotExist**|3727-2146824561 0x800A0E8F|送信先 URL のソース URL または親が存在しません。|  
|**adErrURLNamedRowDoesNotExist**|3737-2146824551 0x800A0E99|この URL によって指定されたレコードは存在しません。|  
|**adErrVolumeNotFound**|3733-2146824555 0x800A0E95|プロバイダーは、URL で示されている記憶装置を見つけることができません。 URL が正しく入力されていることを確認します。|  
|**adErrWriteFile**|3004-2146825284 0x800A0BBC|ファイルへの書き込みに失敗しました。|  
|**adWrnSecurityDialog**|3717-2146824571 0x800A0E85|内部使用のみ。 使用しないでください。|  
|**Adwrnsecurityのヘッダー**|3718-2146824570 0x800A0E86|内部使用のみ。 使用しないでください。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
 次に示す ADO/WFC のサブセットのみが定義されています。  
  
|定数|  
|--------------|  
|AdoEnums. BOUNDTOCOMMAND|  
|AdoEnums DATACONVERSION|  
|AdoEnums FEATURENOTAVAILABLE|  
|AdoEnums ILLEGALOPERATION|  
|AdoEnums. INTRANSACTION|  
|AdoEnums INVALIDARGUMENT|  
|AdoEnums を指定します。 INVALIDCONNECTION|  
|AdoEnums を指定します。 INVALIDPARAMINFO|  
|AdoEnums ITEMNOTFOUND|  
|AdoEnums NOCURRENTRECORD|  
|AdoEnums を実行しています。|  
|AdoEnums. NOTREENTRANT|  
|AdoEnums。 OBJECTCLOSED|  
|AdoEnums の値を指定します。|  
|AdoEnums を指定します。 OBJECTNOTSET|  
|AdoEnums OBJECTOPEN|  
|AdoEnums が取り消されました|  
|AdoEnums PROVIDERNOTFOUND|  
|AdoEnums STILLCONNECTING|  
|AdoEnums STILLEXECUTING|  
|AdoEnums 操作を実行します。|  
  
## <a name="applies-to"></a>適用対象  
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>参照  
 [ADO エラー コード](../../../ado/guide/appendixes/ado-error-codes.md)
