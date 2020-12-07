---
title: PDO::errorCode
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::errorCode 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03ed6428a6c655f3639bd66449506a6e50dd9186
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646182"
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode はデータベース ハンドルの最新の操作の SQLSTATE を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>戻り値  
PDO::errorCode は、5 文字の SQLSTATE を文字列として返すか、データベース ハンドルに操作がない場合、NULL を返されます。  
  
## <a name="remarks"></a>解説  
PDO_SQLSRV ドライバーの PDO::errorCode は、一部の操作の成功時に警告を返します。 たとえば、接続に成功すると、PDO::errorCode は "01000" を返します。これは SQL_SUCCESS_WITH_INFO を示します。  
  
PDO::errorCode は、データベース接続で直接実行された操作のエラー コードのみを返します。 PDO::prepare または PDO::query によって PDOStatement インスタンスを作成する場合、ステートメント オブジェクト上でエラーが生成されると、PDO::errorCode はそのエラーを取得しません。 特定のステートメント オブジェクトで実行された操作のエラー コードを返すには、PDOStatement::errorCode を呼び出す必要があります。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、列の名前が間違っており (`City` ではなく `Cityx`)、エラーが発生します。そのエラーは報告されます。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
