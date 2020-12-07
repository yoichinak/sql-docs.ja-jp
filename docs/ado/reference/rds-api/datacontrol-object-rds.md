---
description: DataControl オブジェクト (RDS)
title: DataControl オブジェクト (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: rothja
ms.author: jroth
ms.openlocfilehash: 81f7d1a3ca15eaf2ebc2bb6dbaff20ba7762d89c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721103"
---
# <a name="datacontrol-object-rds"></a>DataControl オブジェクト (RDS)
データクエリ [レコードセット](../ado-api/recordset-object-ado.md) を1つ以上のコントロール (たとえば、テキストボックス、グリッドコントロール、またはコンボボックス) にバインドして、Web ページに **レコードセット** データを表示します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>解説  
 RDS のクラス ID **。DataControl** オブジェクトは BD96C556-65A3-11D0-983A-00C04FC29E33 です。  
  
> [!NOTE]
>  RDS というエラーが表示される場合 [。領域スペース](./dataspace-object-rds.md) または **RDS。DataControl** オブジェクトが読み込まれません。正しいクラス ID を使用していることを確認してください。 これらのオブジェクトのクラス Id は、バージョン1.0 および1.1 から変更されています。 また、 **RDS DataControl** オブジェクトを使用する場合は、null 値を許容する列も設定する必要があることに注意してください。  
  
 基本的なシナリオでは、RDS の **SQL**、 **Connect**、および **Server** プロパティのみを設定する必要があり **ます。DataControl** オブジェクトは、既定のビジネスオブジェクト [RDSServer DataFactory](./datafactory-object-rdsserver.md)を自動的に呼び出します。  
  
 RDS のすべてのプロパティ **。** カスタムビジネスオブジェクトはその機能を置き換えることができるため、DataControl は省略可能です。  
  
> [!NOTE]
>  複数の結果を照会する場合は、最初の [レコードセット](../ado-api/recordset-object-ado.md) だけが返されます。 複数の結果セットが必要な場合は、それぞれを独自の **DataControl**に割り当てます。 複数の結果を得るためのクエリの例を次に示します。 `"Select * from Authors, Select * from Topics"`  
  
 RDS を使用する場合は、接続文字列に "DFMode = 20;" を追加し **ます。DataControl** オブジェクトを使用すると、データを更新するときにサーバーのパフォーマンスを向上させることができます。 この設定では、サーバー上の **DataFactory** オブジェクトは、より少ないリソースを消費するモードを使用します。 ただし、次の機能はこの構成では使用できません。  
  
-   パラメーター化クエリを使用する。  
  
-   **Execute**メソッドを呼び出す前に、パラメーターまたは列の情報を取得します。  
  
-   **Transact update**を**True**に設定します。  
  
-   行の状態を取得しています。  
  
-   再 [同期](../ado-api/resync-method.md) メソッドを呼び出しています。  
  
-   更新の再 [同期](../ado-api/update-resync-property-dynamic-ado.md) プロパティを使用して (明示的または自動で) 更新します。  
  
-   **コマンド**または[レコードセット](./recordset-sourcerecordset-properties-rds.md)のプロパティを設定します。  
  
-   **Adcmdtabledirect**を使用します。  
  
 **RDS。DataControl**オブジェクトは、既定では非同期モードで実行されます。 アプリケーションの同期実行が必要な場合は、次の例に示すように、 [Executeoptions](./executeoptions-property-rds.md) パラメーターを **Adcexecsync** に、 [Fetchoptions](./fetchoptions-property-rds.md) パラメーターを **adcexecsync**と同じに設定します。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 1つ **の RDS を使用します。** 1 つのクエリの結果を1つ以上のビジュアルコントロールにリンクする DataControl オブジェクトです。 たとえば、顧客データ (名前、居住地、誕生日、年齢、優先度など) を要求するクエリをコーディングするとします。 単一の RDS を使用でき **ます。DataControl** オブジェクトを利用して、顧客の名前、年齢、地域を3つのテキストボックスに表示します。顧客の優先度をチェックボックスで確認します。グリッドコントロールのすべてのデータ。  
  
 別 **の RDS を使用します。DataControl** オブジェクトは、複数のクエリの結果を別のビジュアルコントロールにリンクします。 たとえば、1つのクエリを使用して顧客に関する情報を取得し、2つ目のクエリを使用して、顧客が購入した商品に関する情報を取得するとします。 最初のクエリの結果を3つのテキストボックスと1つのチェックボックスに表示し、2番目のクエリの結果をグリッドコントロールに表示します。 既定のビジネスオブジェクト (**RDSServer. DataFactory**) を使用する場合は、次の操作を行う必要があります。  
  
-   2つ **の RDS を追加します。DataControl** オブジェクトを Web ページに作成します。  
  
-   2つの RDS の各 **SQL** プロパティに1つずつ、2つのクエリを記述 **します。DataControl** オブジェクト。 1つ **の RDS。DataControl** オブジェクトには、顧客情報を要求する SQL クエリが含まれます。2つ目には、顧客が購入した商品の一覧を要求するクエリが含まれます。  
  
-   各バインドコントロールのオブジェクトタグで、DATAFLD 値を指定して、各ビジュアルコントロールに表示するデータの値を設定します。  
  
 RDS の数に制限はありません **。** 1 つの Web ページでオブジェクトタグを使用して埋め込むことができる DataControl オブジェクト。  
  
 RDS を定義する場合 **。** Web ページの DataControl オブジェクトでは、1などの0以外の **高さ** と **幅** の値を使用します (余分なスペースが含まれないようにするため)。  
  
 リモートデータサービスクライアントコンポーネントは、既に Internet Explorer 4.0 の一部として含まれています。したがって、コードベースパラメーターを RDS に含める必要はありません **。DataControl** object タグ。  
  
 Internet Explorer 4.0 以降では、アパートメントモデルコントロールとしてマークされている場合にのみ、HTML コントロールと ActiveX®コントロールを使用してデータにバインドできます。  
  
> [!NOTE]
>  **Microsoft Visual Basic ユーザー****RDS。DataControl**はスクリプトに安全であり、Web ベースのアプリケーションでのみ使用されます。 Visual Basic クライアントアプリケーションには必要ありません。  
  
 ここでは、次のトピックについて説明します。  
  
-   [DataControl オブジェクト (RDS) のプロパティ、メソッド、およびイベント](./datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [DataControl オブジェクトの例 (VBScript)](./datacontrol-object-example-vbscript.md)