---
title: PDO::getAvailableDrivers
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::getAvailableDrivers 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e43ef53820d24128d16ee0f0c7a5d6f1077ff6d2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646622"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PHP のインストールで PDO ドライバーの配列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>戻り値  
PDO ドライバーの一覧が格納された配列。  
  
## <a name="remarks"></a>解説  
PDO ドライバーの名前は、PDO インスタンスを作成するときに PDO::__construct で使用されます。  
  
PHP ドライバーで実行する場合、PDO::getAvailableDrivers は必要ありません。 このメソッドの詳細については、PHP ドキュメントを参照してください。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
