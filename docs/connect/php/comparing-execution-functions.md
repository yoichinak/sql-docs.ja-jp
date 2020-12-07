---
title: 実行関数の比較
description: このトピックでは、Microsoft Drivers for PHP for SQL Server 使用時のさまざまなクエリ実行関数をリストアップします
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680747"
---
# <a name="comparing-execution-functions"></a>実行関数の比較
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、関数を実行するためのいくつかのオプションを提供します。  

## <a name="sqlsrv-execution-functions"></a>SQLSRV 実行関数  
SQLSRV ドライバーを使用している場合、 [sqlsrv_query](../../connect/php/sqlsrv-query.md) を使用して、1 つのクエリを実行し、 [sqlsrv_execute](../../connect/php/sqlsrv-prepare.md) で [sqlsrv_prepare](../../connect/php/sqlsrv-execute.md) を使用して、準備されたステートメントを実行のたびに異なるパラメーター値で複数回実行します。  

## <a name="pdo_sqlsrv-execution-functions"></a>PDO_SQLSRV 実行関数 
PDO_SQLSRV ドライバーを使用している場合は、次のいずれかでクエリを実行できます。  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   「[PDO::prepare](../../connect/php/pdo-prepare.md) 」および「 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)」  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV ドライバー リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)
  
