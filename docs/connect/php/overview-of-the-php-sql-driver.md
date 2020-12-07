---
title: Microsoft Drivers for PHP for SQL Server の概要
description: PHP for SQL Server 用の Microsoft SQLSRV および PDO_SQSRV ドライバーの概要と、データベース アクセス用の PHP アプリケーションでそれらを使用する方法について説明します。
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 556d13a5b29a53b323b41bc9b697d7ad934ca143
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042783"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server の概要

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、Azure SQL Database を含む SQL Server 2005 以降のバージョンにデータ アクセスを提供する、PHP 拡張機能です。 この拡張機能は、SQL Server 2005 以降のすべてのバージョンの SQL Server (Express を含む) でデータにアクセスするための SQLSRV ドライバーとの手続き的なインターフェイスと PDO_SQLSRV ドライバーとのオブジェクト指向のインターフェイスを提供します。 バージョン 3.1 以降のドライバーのサポートは、SQL Server 2008 から開始されます。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API には、Windows 認証、トランザクション、パラメーター バインディング、ストリーミング、メタデータ アクセス、およびエラー処理のサポートが含まれています。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]を使用するには、PHP を実行している同じコンピューターコンピューターに、正しいバージョンの SQL Server Native Client または Microsoft ODBC ドライバーがインストールされている必要があります。  詳細については、「[Microsoft SQL Server 用 Drivers for PHP のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|---------|---------------|  
| ![ダウンロード - 丸で囲んだ下矢印](../../ssms/media/download-icon.png)[PHP for SQL Server のドライバーをダウンロードする](download-drivers-php-sql-server.md) | Microsoft Drivers for PHP for SQL Server をダウンロードするためのリンクです。 |
|[Microsoft SQL Server 用 Drivers for PHP のリリース ノート](../../connect/php/release-notes-php-sql-driver.md)|バージョン 4.0、3.2、3.1、3.0、および 2.0 で追加された機能を示します。|  
|[Microsoft Drivers for PHP for SQL Server 向けのサポート リソース](../../connect/php/support-resources-for-the-php-sql-driver.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]を使用するアプリケーションを開発するときに役立つリソースへのリンクを示します。|  
|[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)|このドキュメントのコード例を実行するときに役立つ情報を提供します。|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>参照先

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV ドライバー リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>参照

[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)  
[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
