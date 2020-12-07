---
description: ODBC 接続プール オプションの設定
title: ODBC 接続プールのオプションを設定する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d6f741654f9765e909a8a2e33bce5e7e596f8b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386598"
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 接続プール オプションの設定
接続プールを使用すると、アプリケーションは、使用するたびに再確立する必要のない接続のプールからの接続を使用できます。 [ **ODBC データソースアドミニストレーター** ] ダイアログボックスの [**接続プール**] タブを使用すると、パフォーマンスの監視を有効または無効にすることができます。 ドライバー名をダブルクリックして、接続のタイムアウト期間を設定します。  
  
 ドライバーレベルでは、CPTimeout レジストリ値によって接続プールが有効になります。 このドライバーごとの選択的な有効化により、システム管理者は、それをサポートするドライバーのみの接続プールを有効にすることができます。 これを行うには、ドライバーのセットアッププログラムの実行中に、CPTimeout の既定値を設定します。 ドライバー名をダブルクリックして、接続のタイムアウト期間を設定します。  
  
 接続プールの詳細については、「 [ODBC 接続プール](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)」を参照してください。  
  
## <a name="performance-monitoring"></a>パフォーマンス監視  
 パフォーマンスの監視では、さまざまな統計情報を記録することで、接続のパフォーマンスを追跡します。 これらの統計情報は、開発者が次のような項目を含めるようにカスタマイズできます。  
  
|カウンター|定義|  
|-------------|----------------|  
|1秒あたりの ODBC ハード接続カウンター|サーバーに対して行われた1秒あたりの実際の接続数。 環境に大きな負荷がかかると、このカウンターは非常に短時間で開始されます。 数秒後に0になります。 これは、接続プールが機能している場合の通常の状況です。 サーバーへの接続が確立されると、それらが使用され、再利用のためにプールに配置されます。|  
|1秒あたりの ODBC ハード切断カウンター|サーバーに対して発行された1秒あたりのハード切断の数。 これらは、接続プールによって解放されるサーバーへの実際の接続です。 システム上のすべてのクライアントを停止し、接続がタイムアウトになると、この値は0から増加します。|  
|1秒あたりの ODBC ソフト接続カウンター|プールによって1秒あたりに満たされた接続の数 (つまり、ユーザーに渡されたそのプールからの接続)。 このカウンターは、プーリングが動作しているかどうかを示します。 サーバーの負荷によっては、1秒あたり40-60 のソフト接続が表示されることは珍しくありません。|  
|1秒あたりの ODBC ソフト切断カウンター|アプリケーションによって発行された切断の1秒あたりの数。 アプリケーションが解放または切断されると、接続はプールに戻されます。|  
|ODBC の現在のアクティブな接続カウンター|プール内で現在使用されている接続の数。|  
|ODBC の現在の空き接続カウンター|プールで使用可能な現在の接続数。 これらは、使用可能なライブ接続です。|  
|現在アクティブなプール|現在アクティブなプールの数。 このカウンターは、接続プール内の接続を管理するドライバー用に Windows 8 で追加されました。 詳細については、「 [ドライバー対応接続プール](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。|  
|作成されたプール|アクティブなプールと削除されたプールを含む、アクティブなプールの数。 このカウンターは、接続プール内の接続を管理するドライバー用に Windows 8 で追加されました。 詳細については、「 [ドライバー対応接続プール](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。|  
  
 独自の監視パラメーターを指定する必要があります。 このバージョンの ODBC には、パフォーマンス監視のサンプルが含まれています。
