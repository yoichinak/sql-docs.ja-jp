---
description: ドライバー マネージャーの接続プール
title: ドライバーマネージャーの接続プール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c3c2fecc26cf2d8bbf5d53598a7b28ce7db5612
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195574"
---
# <a name="driver-manager-connection-pooling"></a>ドライバー マネージャーの接続プール
接続プールを使用すると、アプリケーションは、使用するたびに再確立する必要のない接続のプールからの接続を使用できます。 接続が作成され、プールに配置されると、アプリケーションは、完全な接続プロセスを実行することなく、その接続を再利用できます。  
  
 プールされた接続を使用すると、接続の作成に伴うオーバーヘッドをアプリケーションで節約できるため、パフォーマンスが大幅に向上します。 これは、ネットワーク経由で接続する中間層アプリケーションや、インターネットアプリケーションなどの接続と切断を繰り返すアプリケーションに特に重要です。  
  
 接続プールアーキテクチャを使用すると、パフォーマンスの向上に加えて、1つのプロセスで複数のコンポーネントが環境および関連する接続を使用できるようになります。 これは、同じプロセス内のスタンドアロンコンポーネントが相互に認識されることなく相互に対話できることを意味します。 接続プール内の接続は、複数のコンポーネントで繰り返し使用できます。  
  
> [!NOTE]
>  接続プールは、ODBC 2 を搭載した ODBC アプリケーションで使用できます。アプリケーションが*SQLSetEnvAttr*を呼び出すことができる限り*x*の動作。 接続プールを使用する場合、アプリケーションは、データベースまたはデータベースのコンテキストを変更する SQL ステートメントを実行しないようにする必要があり \<*database name*> ます。たとえば、データソースによって使用されるカタログを変更するを変更します。  


 ODBC ドライバーは完全にスレッドセーフである必要があり、接続プールをサポートするために、接続にスレッドアフィニティを設定することはできません。 つまり、ドライバーは任意のスレッドでの呼び出しをいつでも処理でき、1つのスレッドで接続し、別のスレッドで接続を使用して、3番目のスレッドで切断することができます。  
  
 接続プールは、ドライバーマネージャーによって管理されます。 アプリケーションが **SQLConnect** または **SQLDriverConnect** を呼び出し、アプリケーションが **sqldisconnect**を呼び出したときにプールに返される場合、接続はプールから描画されます。 プールのサイズは、要求されたリソース割り当てに基づいて動的に拡張されます。 非アクティブタイムアウトに基づいて縮小されます。接続が一定期間非アクティブになっている場合 (接続で使用されていない場合)、プールから削除されます。 プールのサイズは、サーバー上のメモリの制約と制限によってのみ制限されます。  
  
 ドライバーマネージャーは、プール内の特定の接続を、 **SQLConnect** または **SQLDriverConnect**で渡された引数に従って使用する必要があるかどうか、および接続が割り当てられた後に設定される接続属性に従って使用するかどうかを決定します。  
  
 ドライバーマネージャーが接続をプールしている場合は、接続がまだ動作しているかどうかを確認してから接続を渡す必要があります。 そうしないと、一時的なネットワーク障害が発生するたびに、ドライバーマネージャーはアプリケーションへの配信不能接続を維持し続けます。 ODBC*3.x: SQL_ATTR_CONNECTION_DEAD*で、新しい接続属性が定義されています。 これは、SQL_CD_TRUE または SQL_CD_FALSE のいずれかを返す読み取り専用の接続属性です。 値 SQL_CD_TRUE は接続が失われたことを意味し、SQL_CD_FALSE の値は、接続がまだアクティブであることを意味します。 (以前のバージョンの ODBC に準拠しているドライバーも、この属性をサポートできます)。  
  
 ドライバーはこのオプションを効率的に実装する必要があります。そうしないと、接続プールのパフォーマンスが低下します。 具体的には、この接続属性の取得を呼び出すと、サーバーへのラウンドトリップが発生しません。 代わりに、ドライバーは接続の最後の既知の状態を返すだけです。 最後のトリップが成功した場合、サーバーへの最後のトリップが失敗した場合、接続は停止していません。  
  
## <a name="remarks"></a>注釈  
 接続が失われた (SQL_ATTR_CONNECTION_DEAD によって報告された) 場合、ODBC ドライバーマネージャーはドライバーで SQLDisconnect を呼び出してその接続を破棄します。 新しい接続要求で、プール内の使用可能な接続が検出されない可能性があります。 最終的には、ドライバーマネージャーはプールが空であると仮定して、新しい接続を作成する可能性があります。  
  
 接続プールを使用するために、アプリケーションは次の手順を実行します。  
  
1.  **SQLSetEnvAttr**を呼び出して接続プールを有効にし、SQL_ATTR_CONNECTION_POOLING 環境属性を SQL_CP_ONE_PER_DRIVER または SQL_CP_ONE_PER_HENV に設定します。 この呼び出しは、アプリケーションが接続プールを有効にする共有環境を割り当てる前に行う必要があります。 **SQLSetEnvAttr**の呼び出しの環境ハンドルは null に設定する必要があります。これにより、プロセスレベルの属性が SQL_ATTR_CONNECTION_POOLING されます。 属性が SQL_CP_ONE_PER_DRIVER に設定されている場合は、ドライバーごとに1つの接続プールがサポートされます。 アプリケーションが多くのドライバーとほとんどの環境で動作する場合、比較が少なくなるため、より効率的な場合があります。 SQL_CP_ONE_PER_HENV に設定すると、環境ごとに1つの接続プールがサポートされます。 アプリケーションが多くの環境で動作し、ドライバーが少ない場合は、比較が少なくなるため、より効率的な場合があります。 SQL_ATTR_CONNECTION_POOLING を SQL_CP_OFF に設定すると、接続プールが無効になります。  
  
2.  *Handletype*引数を SQL_HANDLE_ENV に設定して、 **SQLAllocHandle**を呼び出して環境を割り当てます。 この呼び出しで割り当てられた環境は、接続プールが有効になっているため、暗黙的な共有環境になります。 ただし、使用する環境は、この環境で SQL_HANDLE_DBC の*Handletype* **が呼び出されるまでは**決定されません。  
  
3.  *InputHandle*を SQL_HANDLE_DBC に設定し、 *InputHandle*を接続プールに割り当てられた環境ハンドルに設定して、 **SQLAllocHandle**を呼び出して接続を割り当てます。 ドライバーマネージャーは、アプリケーションによって設定された環境属性に一致する既存の環境の検索を試みます。 このような環境が存在しない場合は、参照カウント (ドライバーマネージャーによって管理されます) が1になるように作成されます。 一致する共有環境が検出されると、環境がアプリケーションに返され、その参照カウントがインクリメントされます。 (実際に使用される接続は、 **SQLConnect** または **SQLDriverConnect** が呼び出されるまでドライバーマネージャーによって決定されることはありません)。  
  
4.  **SQLConnect**または**SQLDriverConnect**を呼び出して接続を確立します。 ドライバーマネージャーは、 **SQLConnect** (または **SQLDriverConnect**の呼び出しの接続キーワード) の呼び出しで接続オプションを使用し、接続の割り当て後に設定された接続属性を使用して、プール内のどの接続を使用する必要があるかを判断します。  
  
    > [!NOTE]  
    >  要求された接続をプールされた接続と照合する方法は、SQL_ATTR_CP_MATCH 環境属性によって決まります。 詳細については、「 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)」を参照してください。  
  
     接続プールを使用する ODBC アプリケーションでは、アプリケーションの初期化中に [CoInitializeEx](/windows/win32/api/combaseapi/nf-combaseapi-coinitializeex) を呼び出し、アプリケーションの終了時に [CoUninitialize](/windows/win32/api/combaseapi/nf-combaseapi-couninitialize) を呼び出す必要があります。  
  
5.  接続の完了時に **Sqldisconnect** を呼び出します。 接続が接続プールに返され、再利用できるようになります。  
  
 詳細については、「 [Microsoft Data Access Components でのプーリング](/previous-versions/ms810829(v=msdn.10))」を参照してください。  
  
## <a name="connection-pooling-considerations"></a>接続プールに関する考慮事項  
 (ODBC API を介してではなく) SQL コマンドを使用して次のアクションを実行すると、接続の状態に影響が生じ、接続プールがアクティブになっている場合に予期しない問題が発生する可能性があります。  
  
-   接続を開き、既定のデータベースを変更します。  
  
-   SET ステートメントを使用して、構成可能なオプション (SET ROWCOUNT、ANSI_NULL、IMPLICIT_TRANSACTIONS、SHOWPLAN、STATISTICS、データセット、および DATEFORMAT) を変更します。  
  
-   一時テーブルとストアドプロシージャを作成する。  
  
 これらのアクションのいずれかが ODBC API 以外で実行された場合、その接続を使用する次のユーザーは、以前の設定、テーブル、またはプロシージャを自動的に継承します。  
  
> [!NOTE]  
>  接続状態に特定の設定が存在しないことを想定しないでください。 アプリケーションでは常に接続状態を設定し、使用されていない接続プール設定がアプリケーションによって削除されるようにする必要があります。  
  
## <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール  
 Windows 8 以降では、ODBC ドライバーがプール内の接続をより効率的に使用できるようになります。 詳細については、「 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データソースまたはドライバーへの接続](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft データアクセスコンポーネントでのプーリング](/previous-versions/ms810829(v=msdn.10))