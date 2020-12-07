---
title: データ型の変換
description: Microsoft Drivers for PHP for SQL Server を使用する場合にデータ型を指定して既定のデータ型に関する詳細を提供する方法について説明します
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 508542ec-cc28-4a17-80f4-52325d6a48db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b72b4e61331754a0bfead58710709552652a176f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680617"
---
# <a name="converting-data-types"></a>データ型の変換
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] では、データを送信するとき、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを取得するときにデータ型を指定できます。 データ型の指定は省略できます。 データ型を指定しない場合、既定の型が使用されます。 このセクションのトピックでは、データ型を指定する方法と既定のデータ型の詳細について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|---------|---------------|  
|[既定の SQL Server のデータ型](../../connect/php/default-sql-server-data-types.md)|サーバーにデータを送信するときの既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型について説明します。|  
|[既定の PHP データ型](../../connect/php/default-php-data-types.md)|サーバーからデータを取得するときの既定の PHP データ型について説明します。|  
|[方法: SQL Server データ型を指定する](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)|サーバーにデータを送信する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を指定する方法について説明します。|  
|[方法:PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)|サーバーからデータを取得するときに PHP データ型を指定する方法について説明します。|  
|[方法:組み込みの UTF-8 サポートを使用した UTF-8 データの送信と取得](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] に備わっている UTF-8 データ サポートを使用する方法について説明します。<br /><br />UTF-8 文字のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のバージョン 1.1 で追加されました。|  
|[方法:Linux および macOS での ASCII データの送信と取得](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)|Linux または macOS で ASCII データに対する [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のサポートを使用する方法を示します。<br /><br />Windows 以外の環境での ASCII 文字のサポートは、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のバージョン 5.2 で追加されました。|
  
## <a name="see-also"></a>参照  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
