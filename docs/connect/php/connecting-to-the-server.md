---
title: サーバーへの接続
description: SQL Server 用 Microsoft Drivers for PHP を使用してデータベースに接続するさまざまな方法について説明します。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a2ec027a72bd96b567b08639568b6ead8e5dc64
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87410978"
---
# <a name="connecting-to-the-server"></a>サーバーへの接続
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このセクションのトピックでは、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するためのオプションと手順について説明します。  

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、Windows 認証または SQL Server 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続できます。 既定では、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は Windows 認証を使用してサーバーへの接続を試みます。  

## <a name="in-this-section"></a>このセクションの内容  

|トピック|説明|  
|---------|---------------|  
|[方法:Windows 認証を使用した接続](../../connect/php/how-to-connect-using-windows-authentication.md)|Windows 認証を使用して接続を確立する方法について説明します。|  
|[方法: SQL Server 認証を使用して接続する](../../connect/php/how-to-connect-using-sql-server-authentication.md)|SQL Server 認証を使用して接続を確立する方法について説明します。|  
|[方法:Azure Active Directory 認証を使用して接続する](../../connect/php/azure-active-directory.md)|認証モードを設定し、Azure Active Directory ID を使用して接続する方法について説明します。|  
|[方法:指定されたポートで接続する](../../connect/php/how-to-connect-on-a-specified-port.md)|特定のポートでサーバーに接続する方法について説明します。|  
|[接続プール](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|ドライバーでの接続プールについて説明します。|  
|[方法:複数のアクティブな結果セット (MARS) を無効にする](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|接続するときに MARS 機能を無効にする方法について説明します。|  
|[接続オプション](../../connect/php/connection-options.md)|接続属性を格納する連想配列で許可されているオプションを示します。|  
|[LocalDB のサポート](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で追加された LocalDB 機能の [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] によるサポートについて説明します。|  
|[高可用性、障害復旧のサポート](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] に追加された高可用性のディザスター リカバリー機能をアプリケーションで利用するための構成方法について説明します。|  
|[Microsoft Azure SQL Database への接続](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Azure SQL Database に接続する方法について説明します。|  
|[接続の回復性](../../connect/php/connection-resiliency.md)|切断された接続を再度確立する接続の回復性機能について説明します。|  

## <a name="see-also"></a>参照  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
