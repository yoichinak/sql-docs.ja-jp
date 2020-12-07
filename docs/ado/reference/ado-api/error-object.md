---
description: Error オブジェクト
title: Error オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: rothja
ms.author: jroth
ms.openlocfilehash: 03f02654e281d052ec8bbb9b8f9df041484cc005
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973663"
---
# <a name="error-object"></a>Error オブジェクト
プロバイダーに関連する1つの操作に関連するデータアクセスエラーの詳細が含まれています。  
  
## <a name="remarks"></a>解説  
 ADO オブジェクトに関連する操作では、1つ以上のプロバイダーエラーが発生することがあります。 各エラーが発生すると、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクションに1つまたは複数の**エラー**オブジェクトが配置されます。 別の ADO 操作によっ**てエラーが**生成されると、 **errors**コレクションがクリアされ、エラーオブジェクトの新しいセットが**errors**コレクションに配置されます。  
  
> [!NOTE]
>  各 **Error** オブジェクトは、ADO エラーではなく、特定のプロバイダーエラーを表します。 ADO エラーは、ランタイム例外処理機構に公開されます。 たとえば、Microsoft Visual Basic で ADO 固有のエラーが発生すると、 **On error** イベントがトリガーされ、 **error** オブジェクトに表示されます。 ADO エラーの完全な一覧については、「 [Errorvalueenum](../../../ado/reference/ado-api/errorvalueenum.md) 」トピックを参照してください。  
  
 次のように、 **エラーオブジェクトのプロパティを読み** 取って、各エラーについての詳細情報を取得できます。  
  
-   [Description](../../../ado/reference/ado-api/description-property.md)プロパティ。エラーのテキストが含まれています。 これは、既定のプロパティです。  
  
-   [Number](../../../ado/reference/ado-api/number-property-ado.md)プロパティ。エラー定数の**長**整数値を格納します。  
  
-   エラーを発生させたオブジェクトを識別する [ソース](../../../ado/reference/ado-api/source-property-ado-error.md) プロパティ。 これは、データソースへの要求に**従ってエラーコレクションに**いくつかの**エラー**オブジェクトがある場合に特に便利です。  
  
-   SQL データソースからの情報を提供する [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) およびの [エラー](../../../ado/reference/ado-api/nativeerror-property-ado.md) プロパティ。  
  
 プロバイダーエラーが発生すると、**接続**オブジェクトの**エラー**コレクションに格納されます。 ADO では、プロバイダー固有のエラー情報を許可するために、1つの ADO 操作で複数のエラーを返すことができます。 エラーハンドラーでこの豊富なエラー情報を取得するには、使用している言語または環境の適切なエラートラップ機能を使用し、入れ子になったループを使用**してエラーコレクション内**の各**エラー**オブジェクトのプロパティを列挙します。  
  
> [!NOTE]
>  **Microsoft Visual Basic と VBScript ユーザー** 有効な **接続** オブジェクトがない場合 **は、エラーオブジェクトから** エラー情報を取得する必要があります。  
  
 プロバイダーと同様に、ADO は、新しいプロバイダーエラーを生成する可能性のある呼び出しを行う前に、 **OLE エラー情報** オブジェクトをクリアします。 ただし、**接続**オブジェクトの**エラー**コレクションは、プロバイダーが新しいエラーを生成したとき、または[Clear](../../../ado/reference/ado-api/clear-method-ado.md)メソッドが呼び出されたときにのみ設定されます。  
  
 一部のプロパティおよびメソッドは、**エラーコレクションに****エラー**オブジェクトとして表示されるが、プログラムの実行を停止しない警告を返します。 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッドを呼び出す前に、**接続**オブジェクトの[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッド。または、**レコードセット**オブジェクトの[Filter](../../../ado/reference/ado-api/filter-property.md)プロパティを設定し、 **Errors**コレクションに対して**Clear**メソッドを呼び出します。 これにより、 **Errors**コレクションの[Count](../../../ado/reference/ado-api/count-property-ado.md)プロパティを読み取って、返された警告をテストできます。  
  
 **エラー**オブジェクトは、スクリプト作成には安全ではありません。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Error オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors コレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
