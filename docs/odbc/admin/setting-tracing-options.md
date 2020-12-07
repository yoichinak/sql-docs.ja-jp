---
description: トレース オプションの設定
title: トレースオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72e3805eded00b1bfa0c984d5ff0ace1ae1494fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476954"
---
# <a name="setting-tracing-options"></a>トレース オプションの設定
[ **Odbc データソースアドミニストレーター** ] ダイアログボックスの [**トレース**] タブを使用すると、odbc 関数呼び出しをトレースする方法を構成できます。  
  
## <a name="how-tracing-works"></a>トレースのしくみ  
 [ **トレース** ] タブからトレースを開始すると、ドライバーマネージャーは、その後実行されるすべての ODBC 関数呼び出しをログに記録します。 トレースが開始される前に実行されているアプリケーションからの ODBC 関数呼び出しはログに記録されません。 ODBC 関数の呼び出しは、指定したログファイルに記録されます。  
  
 トレースは、[トレースの **停止**] をクリックした後にのみ停止します。 トレースが有効になっている間は、ログファイルが増加し続け、すべての ODBC アプリケーションのパフォーマンスに影響することに注意してください。  
  
 トレースの詳細については、「 [トレース](../../odbc/reference/develop-app/tracing.md)」を参照してください。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC トレースの変更点  
 MDAC 2.7 SP2 より前のバージョンでは、ODBC トレースはコンピューター全体に対してのみ実行することが許可されていました。この場合、トレースによって、任意の id で実行されているすべての ODBC アプリケーションに関する詳細情報が公開されます。 これには、他のローカルユーザーアカウントの代わりに作成または実行されるプロセス、またはローカルサービスやネットワークサービスなどの組み込みのセキュリティプリンシパルに代わって作成または実行されるプロセスで発生する可能性がある、ODBC 関連のアクティビティのトレースが含まれます。  
  
 既定では、ODBC トレースはユーザーごとのモードを使用するようになりました。 ただし、ローカル管理者の場合でも、ODBC データソースアドミニストレーターを使用して、コンピューター全体のトレースを有効にすることができます。  
  
 ODBC トレースモードを構成するには、次のようにします。  
  
1.  必要に応じて、ローカルの Administrators グループのメンバーシップを持つアカウントを使用してログオンします。  
  
2.  [管理ツール] から、ODBC データソースアドミニストレーターを開きます。  
  
3.  **[トレース]** タブをクリックします。  
  
4.  [ **すべてのユーザー id に対してコンピューター全体のトレース** を使用する] チェックボックスを使用して、トレースモードを構成します。  
  
5.  コンピューター全体のトレースを有効にするには、チェックボックスをオンにします。  
  
6.  ユーザーごとのトレースに戻るには、このチェックボックスをオフにします。  
  
7.  **[適用]** をクリックします。  
  
> [!NOTE]  
>  1つのモードで既にトレースを開始している場合は、トレースを停止し、モードを正常に変更するために他のモードに切り替える必要があります。  
  
> [!IMPORTANT]  
>  コンピューター全体のトレースは、必要な場合にのみ有効にする必要があります。それ以外の場合は、オフのままにする必要があります。  
  
## <a name="visual-studio-analyzer-tracing"></a>トレースの Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer のサポートは、Windows 8 以降で削除されました (Visual Studio Analyzer 以前のバージョンの Visual Studio にのみ含まれていました)。 別のトラブルシューティングメカニズムについては、BID トレースを使用します。  
  
 Visual Studio® Analyzer トレースでは、ODBC レイヤーに関するパフォーマンスとデバッグ情報が提供されます。 すべての送信イベントは、ODBC コンポーネントで費やされた時間について、可能な限り正確な画像として表示される最上位レベルのインターフェイスで発生します。 Visual Studio Analyzer のトレースでは、ソースの設定時にイベントソースを登録する必要があります。 この種類のトレースの詳細については、Visual Studio のドキュメントを参照してください。
