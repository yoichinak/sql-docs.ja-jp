---
description: ODBC ドライバー対応接続プールの開発
title: ODBC ドライバーでの Connection-Pool 認識の開発 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f22be001a7434c13158deae8677b8c7bcb2f0630
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192312"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC ドライバー対応接続プールの開発
このトピックでは、ドライバーが接続プールサービスを提供する方法に関する情報を含む ODBC ドライバーの開発の詳細について説明します。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Driver-Aware 接続プールの有効化  
 ドライバーは、次の ODBC サービスプロバイダーインターフェイス (SPI) 関数を実装する必要があります。  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 詳細については、「 [ODBC サービスプロバイダインターフェイス (SPI) リファレンス](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 」を参照してください。  
  
 ドライバーが対応するプールを有効にするには、次の既存の関数も実装する必要があります。  
  
|関数|追加された機能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|新しいハンドルの種類をサポートしています: SQL_HANDLE_DBC_INFO_TOKEN (以下の説明を参照してください)。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|新しいセットのみの接続属性をサポートする: 接続をリセットするための SQL_ATTR_DBC_INFO_TOKEN ます (以下の説明を参照してください)。|  
  
> [!NOTE]  
>  **SQLError**や**SQLSetConnectOption**などの非推奨の関数は、ドライバー対応の接続プールではサポートされていません。  
  
## <a name="the-pool-id"></a>プール ID  
 プール ID は、相互に使用できる特定の接続グループを表す、ポインター長のドライバー固有の ID です。 接続情報のセットを指定すると、ドライバーは対応するプール ID をすばやく推測できる必要があります。  
  
 たとえば、プール ID はサーバー名と資格情報をエンコードする必要があります。 ただし、ドライバーが接続を再利用して、新しい接続を作成するよりも短時間でデータベースを変更できるため、データベース名は必要ありません。  
  
 ドライバーは、一連のキー属性を定義する必要があります。これにより、プール ID が構成されます。 これらのキー属性の値は、接続属性、接続文字列、および DSN から取得できます。 これらのソースに競合がある場合は、既存のドライバー固有の解決ポリシーを旧バージョンとの互換性のために使用する必要があります。  
  
 ドライバーマネージャーは、プール Id によって異なるプールを使用します。 同じプール内のすべての接続は再利用できます。 ドライバーマネージャーは、別のプール ID を持つ接続を再利用することはありません。  
  
 したがって、ドライバーは、定義されたキー属性の値が同じである接続のグループごとに一意のプール ID を割り当てる必要があります。 ドライバーでキー属性の値が異なる2つの接続に同じプール ID が使用されている場合、ドライバーマネージャーはそれらを同じプールに配置します (ドライバーマネージャーは、ドライバー固有のキー属性については何も認識しません)。 これは、別のキー属性セットとの接続が [SQLRateConnection 関数](../../../odbc/reference/syntax/sqlrateconnection-function.md)内で再利用できないことをドライバーマネージャーに報告する必要があることを意味します。 これにより、パフォーマンスが低下する可能性があります。これは推奨されません。  
  
 ドライバーマネージャーは、すべての接続情報が一致する場合でも、別のドライバー環境から割り当てられた接続を再利用しません。 ドライバーマネージャーは、接続に同じプール ID が割り当てられている場合でも、異なる環境に対して異なるプールを使用します。 そのため、プール ID はドライバー環境に対してローカルです。  
  
 ドライバーからプール ID を取得するための関数は、 [SQLGetPoolID 関数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)です。  
  
## <a name="the-connection-rating"></a>接続の評価  
 新しい接続の確立と比較すると、プールされた接続の一部の接続情報 (データベースなど) をリセットすることで、パフォーマンスを向上させることができます。 したがって、キー属性のセットにデータベース名を含めることはできません。 そうしないと、データベースごとに個別のプールを作成できます。これは、顧客がさまざまな接続文字列を使用する中間層アプリケーションでは適切ではない可能性があります。  
  
 属性の不一致がある接続を再利用する場合は常に、新しいアプリケーションの要求に基づいて一致しない属性をリセットし、返された接続がアプリケーションの要求と同一になるようにします ( [SQLSetConnectAttr 関数](../syntax/sqlsetconnectattr-function.md)の属性 SQL_ATTR_DBC_INFO_TOKEN の説明を参照してください)。 ただし、これらの属性をリセットすると、パフォーマンスが低下する可能性があります。 たとえば、データベースをリセットするには、サーバーへのネットワーク呼び出しが必要です。 そのため、完全に一致する接続を再利用できます (使用可能な場合)。  
  
 ドライバーの評価関数は、新しい接続要求で既存の接続を評価できます。 たとえば、ドライバーの評価機能は次のことを判断できます。  
  
-   既存の接続が要求と完全に一致する場合はです。  
  
-   接続のタイムアウトなど、いくつかの重要でない不一致のみがある場合は、サーバーとの通信をリセットする必要はありません。  
  
-   サーバーとの通信を必要とする属性が一致しない場合でも、新しい接続を確立するよりもパフォーマンスが向上します。  
  
-   リセットに非常に時間がかかる属性で不一致が発生した場合 (ドライバーの開発者は、プール ID の生成に使用されるキー属性のセットにこの属性を追加することを検討できます)。  
  
 0 ~ 100 の間のスコアは可能です。0は再利用されず、100は完全に一致することを意味します。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) は、接続を評価する関数です。  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>新しい ODBC ハンドル-SQL_HANDLE_DBC_INFO_TOKEN  
 ドライバー対応接続プールをサポートするには、ドライバーがプール ID を計算するために接続情報を必要とします。 また、ドライバーは、新しい接続要求とプール内の接続を比較するための接続情報も必要です。  プール内の接続を再利用できない場合、ドライバーは新しい接続を確立する必要があるため、接続情報が必要になります。  
  
 接続情報は複数のソース (接続文字列、接続属性、DSN) から取得できるため、ドライバーは接続文字列を解析し、上記の関数呼び出しごとにこれらのソース間の競合を解決することが必要になる場合があります。  
  
 そのため、新しい ODBC ハンドルが導入されています。 SQL_HANDLE_DBC_INFO_TOKEN。 SQL_HANDLE_DBC_INFO_TOKEN では、ドライバーは接続文字列を解析し、接続情報の競合を複数回解決する必要はありません。 これはドライバー固有のデータ構造であるため、ドライバーは接続情報やプール ID などのデータを格納できます。  
  
 このハンドルは、ドライバーマネージャーとドライバーの間のインターフェイスとしてのみ使用されます。 アプリケーションがこのハンドルを直接割り当てることはできません。  
  
 このハンドルの親ハンドルの種類は SQL_HANDLE_ENV であり、ドライバーは接続情報の解決中に HENV ハンドルから環境情報を取得できます。  
  
 ドライバーマネージャーは、新しい接続要求を受信するたびに、接続プールの認識をサポートしていることを確認した後、接続情報を格納するための SQL_HANDLE_DBC_INFO_TOKEN 種類のハンドルを割り当てます。 ハンドルの使用が終了したとき (ただし、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) または [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)からの SQL_STILL_EXECUTING 以外のリターンコードを返す前) は、ドライバーマネージャーによってハンドルが解放されます。 したがって、ハンドルは SQLAllocHandle 呼び出しの後に作成され、SQLFreeHandle 呼び出しの後に破棄されます。 ドライバーマネージャーは、関連付けられている HENV を解放する前にハンドルが解放されることを保証します ( [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) または [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) がエラーを返す場合)。  
  
 ドライバーは、新しいハンドル型 SQL_HANDLE_DBC_INFO_TOKEN を受け入れるように次の関数を変更する必要があります。  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 ドライバーマネージャーは、複数のスレッドが同時に同じ SQL_HANDLE_DBC_INFO_TOKEN ハンドルを使用しないことを保証します。 このため、このハンドルの同期モデルはドライバー内で非常に単純にすることができます。 ドライバーマネージャーは、SQL_HANDLE_DBC_INFO_TOKEN を割り当てて解放する前に、環境ロックを取得しません。  
  
 ドライバーマネージャーの **SQLAllocHandle** と **sqlfreehandle** は、この新しいハンドルの種類を受け入れません。  
  
 SQL_HANDLE_DBC_INFO_TOKEN には、資格情報などの機密情報が含まれている場合があります。 そのため、ドライバーは、 **Sqlfreehandle**でこのハンドルを解放する前に、機密情報を格納するメモリバッファー ( [secureゼロメモリ](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)を使用) を安全にクリアする必要があります。 アプリケーションの環境ハンドルを閉じるたびに、関連付けられているすべての接続プールが閉じられます。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>ドライバーマネージャーの接続プールの評価アルゴリズム  
 このセクションでは、ドライバーマネージャーの接続プールの評価アルゴリズムについて説明します。 ドライバー開発者は、旧バージョンとの互換性のために同じアルゴリズムを実装できます。 このアルゴリズムは最適ではない場合があります。 このアルゴリズムは、実装に基づいて調整する必要があります (それ以外の場合は、この機能を実装する理由はありません)。  
  
 ドライバーマネージャーは、プールからの各接続について、0 ~ 100 の整数評価を返します。 0は、接続を再利用できないことを意味し、100は完全に一致することを示します。 接続要求に hRequest という名前を付け、プールからの既存の接続に Hrequest という名前を付けているとします。 次のいずれかの条件が false の場合、プールされた接続の hCandidate を Hcandidate に再利用することはできません (ドライバーマネージャーによって0という評価が割り当てられます)。  
  
-   hCandidate と Hcandidate はどちらも、UNICODE API (SQLDriverConnectW など) または ANSI API (SQLDriverConnectA など) から取得されます。 (UNICODE ドライバーの動作は、ANSI API と UNICODE API によって異なります (接続属性の SQL_ATTR_ANSI_APP を参照してください)。  
  
-   hCandidate と Hcandidate は同じ関数によって作成されます。SQLDriverConnect または SQLConnect のいずれかです。  
  
-   SQLDriverConnect が使用されている場合、hCandidate を開くために使用する接続文字列は Hcandidate と同じである必要があります。  
  
-   HCandidate を開くために使用される ServerName (または DSN)、ユーザー名、およびパスワードは、SQLConnect が使用されているときに Hcandidate を開くために使用されるものと同じである必要があります。  
  
-   現在のスレッドのセキュリティ識別子 (SID) は、hCandidate を開くために使用される SID と同じである必要があります。  
  
-   参加と参加解除にかかるコストが高いドライバー ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)の SQL_DTC_TRANSITION_COST の説明を参照) については、 *hrequest* を再利用する場合、追加の参加または参加解除は必要ありません。  
  
 次の表は、さまざまなシナリオのスコア割り当てを示しています。  
  
|プールされた接続と要求の間の接続属性の比較|参加解除/参加解除|追加の参加/参加解除が必要|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|カタログ (SQL_ATTR_CURRENT_CATALOG) が異なります|60|50|  
|一部の接続属性は異なっていますが、catalog は同じです。|90|70|  
|完全に一致したすべての接続属性|100|80|  
  
## <a name="sequence-diagram"></a>シーケンス図  
 このシーケンス図は、このトピックで説明する基本的なプーリングメカニズムを示しています。 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)の使用のみが表示されますが、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)ケースは似ています。  
  
 ![シーケンス図](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状態ダイアグラム  
 この状態の図は、このトピックで説明する接続情報トークンオブジェクトを示しています。 図には [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) のみが表示されますが、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) のケースは似ています。 ドライバーマネージャーは、いつでもエラーを処理する必要があるため、ドライバーマネージャーは [Sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) を任意の状態に対して呼び出すことができます。  
  
 ![状態の図](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>参照  
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC サービス プロバイダー インターフェイス (SPI) リファレンス](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)