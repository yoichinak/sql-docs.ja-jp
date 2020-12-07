---
description: ODBC サービス プロバイダー インターフェイス (SPI) リファレンス
title: ODBC サービスプロバイダーインターフェイス (SPI) リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ef1eea6dd78537169d3394c7d048d1829e8d9a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487355"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC サービス プロバイダー インターフェイス (SPI) リファレンス
従来、ODBC では、アプリケーションプログラミングインターフェイス (API) が定義されていました。 API 内の関数は、アプリケーションから呼び出すことができ、ドライバーマネージャーとドライバーの両方で実装する必要があります。  
  
 ODBC では、ドライバー対応の接続プール機能が追加され、service provider interface (SPI) が導入されています。 SPI 内の関数は、ドライバーマネージャーとドライバーの間の通信に使用されます。 SPI 関数はドライバーによって実装されます。ドライバーマネージャーは、アプリケーションに対して SPI 関数を公開しません。 アプリケーションはこれらの関数を直接呼び出すことはできません。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
 このセクションでは、以下のトピックについて説明します。  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ODBC ドライバーでの接続プール認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [ドライバー マネージャーの接続プール](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
