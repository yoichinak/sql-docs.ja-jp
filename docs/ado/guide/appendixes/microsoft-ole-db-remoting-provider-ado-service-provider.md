---
description: Microsoft OLE DB リモート処理プロバイダー (ADO サービスプロバイダー)
title: Microsoft OLE DB リモート処理プロバイダー (ADO サービスプロバイダー) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a4e4fcec5217a9a9475f11d3a386c7436892ea6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724873"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB リモート処理プロバイダーの概要
Microsoft OLE DB リモート処理プロバイダーを使用すると、クライアントコンピューターのローカルユーザーは、リモートコンピューター上のデータプロバイダーを呼び出すことができます。 リモートコンピューターのローカルユーザーの場合と同様に、リモートコンピューターのデータプロバイダーパラメーターを指定します。 次に、リモートコンピューターにアクセスするためにリモート処理プロバイダーによって使用されるパラメーターを指定します。 これにより、ローカルユーザーと同じようにリモートコンピューターにアクセスできます。

> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、  [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。

## <a name="provider-keyword"></a>Provider キーワード
 OLE DB リモート処理プロバイダーを呼び出すには、接続文字列に次のキーワードと値を指定します。 (プロバイダー名の空白部分に注意してください)。

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>その他のキーワード
 このサービスプロバイダーが呼び出されると、次の追加のキーワードが関連します。

|Keyword|説明|
|-------------|-----------------|
|**データ ソース**|リモートデータソースの名前を指定します。 これは、処理のために OLE DB リモート処理プロバイダーに渡されます。<br /><br /> このキーワードは、RDS に相当し [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクトの [Connect](../../reference/rds-api/connect-property-rds.md) プロパティ。|

## <a name="dynamic-properties"></a>動的プロパティ
 このサービスプロバイダーが呼び出されると、次の動的プロパティが [接続](../../reference/ado-api/connection-object-ado.md)オブジェクトの [properties](../../reference/ado-api/properties-collection-ado.md) コレクションに追加されます。

|動的プロパティ名|説明|
|---------------------------|-----------------|
|**DFMode**|DataFactory モードを示します。 サーバー上の [DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) オブジェクトの目的のバージョンを指定する文字列です。 **DataFactory**の特定のバージョンを要求する接続を開く前に、このプロパティを設定します。 要求されたバージョンを使用できない場合は、前のバージョンを使用しようとします。 前のバージョンがない場合は、エラーが発生します。 **DFMode**が使用可能なバージョンよりも小さい場合は、エラーが発生します。 このプロパティは、接続が確立された後に読み取り専用になります。<br /><br /> には、次の有効な文字列値のいずれかを指定できます。<br /><br /> -"25"-バージョン 2.5 (既定)<br />-"21"-バージョン2.1<br />-"20"-バージョン2.0<br />-"15"-バージョン1.5|
|**コマンドのプロパティ**|MS リモートプロバイダーによってサーバーに送信されるコマンド (行セット) プロパティの文字列に追加される値を示します。 この文字列の既定値は vt_empty です。|
|**現在の DFMode**|サーバー上の **DataFactory** の実際のバージョン番号を示します。 **DFMode**プロパティで要求されたバージョンが受け入れられたかどうかを確認するには、このプロパティをオンにします。<br /><br /> 次の有効な長整数値のいずれかを指定できます。<br /><br /> -25-バージョン 2.5 (既定)<br />-21-バージョン2.1<br />-20-バージョン2.0<br />-15-バージョン1.5<br /><br /> **Msremote**プロバイダーの使用時に接続文字列に "DFMode = 20;" を追加すると、データを更新するときのサーバーのパフォーマンスが向上します。 この設定では、サーバー上の **DataFactory** オブジェクトは、より少ないリソースを消費するモードを使用します。 ただし、次の機能はこの構成では使用できません。<br /><br /> -パラメーター化クエリの使用。<br />- **Execute** メソッドを呼び出す前に、パラメーターまたは列の情報を取得します。<br />- **Transact update** を **True**に設定します。<br />-行の状態を取得しています。<br />-再 **同期** メソッドを呼び出しています。<br />- **更新プログラム** の再同期プロパティを使用して (明示的または自動で) 更新します。<br />- **コマンド** または **レコードセット** のプロパティを設定します。<br />- **Adcmdtabledirect**を使用します。|
|**Handler**|[RDSServer](../../reference/rds-api/datafactory-object-rdsserver.md)の機能を拡張するサーバー側のカスタマイズプログラム (またはハンドラー) の名前、およびハンドラーで使用されるすべてのパラメーターをコンマ (",") で区切って指定します。 **文字列**値です。|
|**インターネットタイムアウト**|サーバーとの間での要求の移動を待機する最大時間 (ミリ秒単位) を示します。 (既定値は5分です)。|
|**リモートプロバイダー**|リモートサーバーで使用されるデータプロバイダーの名前を示します。|
|**リモートサーバー**|この接続で使用されるサーバー名と通信プロトコルを示します。 このプロパティは、RDS に相当し [ます。DataContro](../../reference/rds-api/datacontrol-object-rds.md) Object [サーバー](../../reference/rds-api/server-property-rds.md) プロパティ。|
|**更新プログラム**|**True**に設定すると、この値は、 [UpdateBatch](../../reference/ado-api/updatebatch-method.md)がサーバーで実行されるときに、トランザクション内で実行されることを示します。 このブール型の動的プロパティの既定値は **False**です。|

 接続文字列のキーワードとして名前を指定して、書き込み可能な動的プロパティを設定することもできます。 たとえば、次のように指定して、 **Internet Timeout** 動的プロパティを5秒に設定します。

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 また、プロパティの名前を **Properties** プロパティのインデックスとして指定して、動的プロパティを設定または取得することもできます。 次の例は、 **Internet Timeout** 動的プロパティの現在の値を取得して印刷し、新しい値を設定する方法を示しています。

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>解説
 ADO 2.0 では、OLE DB リモート処理プロバイダーは、 [Recordset](../../reference/ado-api/recordset-object-ado.md)オブジェクト**Open**メソッドの*ActiveConnection*パラメーターでのみ指定できました。 ADO 2.1 以降では、[接続](../../reference/ado-api/connection-object-ado.md)オブジェクト**Open**メソッドの*ConnectionString*パラメーターでプロバイダーを指定することもできます。

 RDS に相当する **。DataControl** Object [SQL](../../reference/rds-api/sql-property.md) プロパティは使用できません。 代わりに、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクト **Open** method *Source* 引数が使用されます。

 **メモ** "..." を指定します。リモートプロバイダー = MS Remote;... "では、4層のシナリオを作成します。 3層を超えるシナリオはテストされていないため、必要ありません。

## <a name="example"></a>例
 この例では、*サーバー*という名前のサーバー上にある**Pubs**データベースの**Authors**テーブルに対してクエリを実行します。 リモートデータソースとリモートサーバーの名前は[接続](../../reference/ado-api/connection-object-ado.md)オブジェクトの[open](../../reference/ado-api/open-method-ado-connection.md)メソッドに指定され、SQL クエリは[Recordset](../../reference/ado-api/recordset-object-ado.md)オブジェクトの[open](../../reference/ado-api/open-method-ado-recordset.md)メソッドに指定されます。 **レコードセット**オブジェクトが返され、編集されて、データソースを更新するために使用されます。

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>参照
 [OLE DB リモート処理プロバイダーの概要](/previous-versions/windows/desktop/ms713673(v=vs.85))