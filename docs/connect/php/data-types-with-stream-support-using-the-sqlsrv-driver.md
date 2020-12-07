---
title: SQLSRV ドライバーを使用したストリームでのデータ型のサポート
description: このトピックでは、Microsoft SQLSRV Driver for PHP for SQL Server の使用時、ストリームとして取得できる SQL Server データ型をリストアップします
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- streaming data
ms.assetid: a16fe7da-e4c8-45f5-be54-aad03c4fa168
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ca74b31b55fd0cb8a0c8405ac3303d041c38478
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680807"
---
# <a name="data-types-with-stream-support-using-the-sqlsrv-driver"></a>SQLSRV ドライバーを使用したストリームでのデータ型のサポート
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ストリームとしてのデータの取得は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーでのみ使用でき、PDO_SQLSRV ドライバーでは使用できません。  
  
次の SQL Server のデータ型は、SQLSRV ドライバーを使用して、ストリームとして取得することができます。  
  
-   binary  
  
-   char  
  
-   image  
  
-   nchar  
  
-   ntext  
  
-   nvarchar  
  
-   text  
  
-   UDT  
  
-   varbinary  
  
-   varchar  
  
-   XML  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバーを使用してデータをストリームとして取得する](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[既定の PHP データ型](../../connect/php/default-php-data-types.md)

[方法:PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)  
  
