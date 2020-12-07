---
description: Open メソッド (ADO Record)
title: Open メソッド (ADO Record) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ad606821e423892d49feb49a0920c7aea9056aa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990343"
---
# <a name="open-method-ado-record"></a>Open メソッド (ADO Record)
既存の [レコード](./record-object-ado.md) オブジェクトを開くか、ファイルやディレクトリなどの **レコード**によって表される新しい項目を作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 この**レコード**オブジェクトによって表されるエンティティの URL、**コマンド**、開いているレコード[セット](./recordset-object-ado.md)または別の**レコード**オブジェクト、SQL SELECT ステートメントまたはテーブル名を含む文字列を表す**バリアント**。  
  
 *ActiveConnection*  
 省略可能。 接続文字列または開いている[接続](./connection-object-ado.md)オブジェクトを表す**バリアント**です。  
  
 *モード*  
 省略可能。 結果の**レコード**オブジェクトのアクセスモードを指定する[connectmodeenum](./connectmodeenum.md)値です。 既定値は **Admodeunknown**です。  
  
 *CreateOptions*  
 省略可能。 既存のファイルまたはディレクトリを開くか、新しいファイルまたはディレクトリを作成する必要があるかを指定する [Recordcreateoptionsenum](./recordcreateoptionsenum.md) 値。 既定値は **Adfailifnotexists**です。 既定値に設定されている場合、アクセスモードは [mode](./mode-property-ado.md) プロパティから取得されます。 *Source*パラメーターに URL が含まれていない場合、このパラメーターは無視されます。  
  
 *Options*  
 省略可能。 **レコード**を開くためのオプションを指定する[RecordOpenOptionsEnum](./recordopenoptionsenum.md)値です。 既定値は **Adopenrecordunspecified**です。 これらの値は組み合わせることができます。  
  
 *UserName*  
 省略可能。 必要に応じて、*ソース*へのアクセスを承認するユーザー ID を表す**文字列**値です。  
  
 *パスワード*  
 省略可能。 必要に応じて*ユーザー名*を確認するパスワードを含む**文字列**値です。  
  
## <a name="remarks"></a>解説  
 *ソース* は次のようになります。  
  
-   URL。 URL のプロトコルが http の場合、インターネットプロバイダーが既定で呼び出されます。 URL が、のような実行可能スクリプトを含むノードを指している場合は。ASP ページ) 既定では、実行されたコンテンツではなく、ソースを含む **レコード** が開かれます。 この動作を変更するには、 *Options* 引数を使用します。  
  
-   **レコード**オブジェクト。 別の**レコード**から開かれた**レコード**オブジェクトは、元の**レコード**オブジェクトを複製します。  
  
-   **コマンド**オブジェクト。 開いている **レコード** オブジェクトは、 **コマンド**の実行によって返される単一行を表します。 結果に1つ以上の行が含まれている場合は、最初の行の内容がレコードに配置され **、エラーがエラーコレクションに** 追加されることがあります。  
  
-   SQL SELECT ステートメント。 開いている **レコード** オブジェクトは、文字列の内容を実行して返される単一行を表します。 結果に1つ以上の行が含まれている場合は、最初の行の内容がレコードに配置され **、エラーがエラーコレクションに** 追加されることがあります。  
  
-   テーブル名。  
  
 **レコード**オブジェクトが、URL を使用してアクセスできないエンティティ (たとえば、データベースから派生した**レコードセット**の行) を表している場合、 [parenturl](./parenturl-property-ado.md)プロパティと**adRecordURL**定数でアクセスされるフィールドの両方の値は null になります。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Connection)](./open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](./open-method-ado-stream.md)   
 [OpenSchema メソッド](./openschema-method.md)