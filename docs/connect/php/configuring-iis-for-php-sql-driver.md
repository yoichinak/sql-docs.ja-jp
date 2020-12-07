---
title: Drivers for PHP 用の IIS の構成
description: Drivers for PHP for SQL Server を使用する PHP アプリケーションをホストするように IIS を構成する方法について説明します。 ここに示すリソースは、IIS での FastCGI の使用に固有のものです。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ab31be628d4c93f0e4331e3d63d47c4924a6fa7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726884"
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>SQL Server 用 Microsoft Drivers for PHP に対する IIS の構成
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、PHP アプリケーションをホストするための IIS の構成に関連のある[インターネット インフォメーション サービス (IIS) Web サイト](https://www.iis.net/)上のリソースへのリンクを提供します。 ここに示すリソースは、IIS での FastCGI の使用に固有のものです。 FastCGI は、アプリケーション フレームワークの Common Gateway Interface (CGI) の実行可能ファイルが Web サーバーとやり取りできる標準プロトコルです。 FastCGI は、標準の CGI プロトコルとは異なり、CGI プロセスを複数の要求に再使用します。  
  
## <a name="tutorials"></a>チュートリアル  
次のリンクは、PHP 用の FastCGI の設定、および IIS 6.0 と IIS 7.0 での PHP アプリケーションのホストに関するチュートリアルに対するものです。  
  
-   [PHP での FastCGI](/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [IIS 7.0 で PHP アプリケーションをホストするための FastCGI の使用](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [IIS 6.0 で PHP アプリケーションをホストするための FastCGI の使用](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [IIS 6.0 用の FastCGI 拡張機能の構成](/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>ビデオ プレゼンテーション  
次のリンクは、PHP 用の FastCGI の設定、および IIS 7.0 機能を使用した PHP アプリケーションのホストに関するビデオ プレゼンテーションに対するものです。  
  
-   [PHP 用の FastCGI の設定](/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [Microsoft インターネット インフォメーション サービス 7 での PHP とのパーティー](/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>サポート リソース  
次のフォーラムでは、IIS での FastCGI に対するコミュニティ サポートが提供されます。  
  
-   [FastCGI ハンドラー](https://forums.iis.net/1103.aspx)  
-   [IIS 7 - FastCGI モジュール](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>参照  
[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
