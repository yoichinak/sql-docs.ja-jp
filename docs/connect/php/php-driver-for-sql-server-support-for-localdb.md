---
title: PHP ドライバーによる LocalDB のサポート
description: Microsoft SQL Server 用 Drivers for PHP で LocalDB データベース インスタンスへの接続がどのようにサポートされるかについて説明します。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47bcfa16712e0ef227da7c7ae53de14aa42deacb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726773"
---
# <a name="support-for-localdb"></a>LocalDB のサポート

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の軽量バージョンで、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から使用できるようになりました。 ここでは、LocalDB インスタンス内のデータベースに接続する方法について説明します。

## <a name="remarks"></a>解説

LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB に関する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックのトピックを参照してください。

要約すると、LocalDB では、次のことを行うことができます。

-   **sqllocaldb.exe i** を使用して既定のインスタンスの名前を検出できます。

-   **AttachDBFilename** 接続文字列キーワードを使用して、サーバーをアタッチするデータベース ファイルを指定できます。 **AttachDBFilename** を使用するときに、**Database** 接続文字列キーワードを使用してデータベース名を指定しなかった場合、データベースはアプリケーションの終了時に LocalDB インスタンスから削除されます。

-   接続文字列では、次のように LocalDB インスタンスを指定します。 例として、サンプルの SQLSRV 接続文字列を次に示します。

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    次に示すのは、サンプルの PDO_SQLSRV 接続文字列です。  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

必要に応じて、sqllocaldb.exe を使用して LocalDB インスタンスを作成できます。 また、sqlcmd.exe を使用して、LocalDB インスタンスのデータベースの追加と変更を実行できます。 たとえば、「 `sqlcmd -S (localdb)\v11.0` 」のように入力します。 (IIS で実行する場合、コマンド ラインで実行する場合と同じ結果を得るには、正しいアカウントで実行する必要があります。詳細については、「[完全 IIS での LocalDB の使用、第 2 部: インスタンスの所有権](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership)」を参照してください。

次に示す接続文字列の例では、SQLSRV ドライバーを使用して、myInstance という名前の LocalDB 名前付きインスタンス内のデータベースに接続します。

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

次に示す接続文字列の例では、PDO_SQLSRV ドライバーを使用して、myInstance という名前の LocalDB 名前付きインスタンス内のデータベースに接続します。  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

LocalDB のインストール手順については、[LocalDB のドキュメント](../../database-engine/configure-windows/sql-server-express-localdb.md)を参照してください。 sqlcmd.exe を使用して LocalDB インスタンス内のデータを変更する場合、[sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)が必要です。

## <a name="see-also"></a>参照

[サーバーへの接続](../../connect/php/connecting-to-the-server.md)