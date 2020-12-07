---
title: システム ロケール以外の設定
description: Linux と macOS のさまざまなロケール設定が Microsoft Drivers for PHP for SQL Server に与える影響について説明します
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 303037729164d4165fc106529a901b58d4d049f4
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680527"
---
# <a name="non-system-locale-settings"></a>システム ロケール以外の設定
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このセクションは、Linux および macOS ユーザー、特に php アプリケーションで複数のロケールを扱うユーザーにのみ適用されます。

既定で [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] はシステムで定義された `LC_ALL` 環境変数を受け取り、他のすべての `LC_xxx` カテゴリ (状況によっては `$LANG` または `$LANGUAGE` を除く) がオーバーライドされます。これは、桁区切り記号、小数点、文字セット、月、日の名前、エラー メッセージなどのアプリケーション メッセージ、通貨記号などに影響があります。

バージョン 5.8.0 以降では、次の例に示すように、ユーザーは php.ini ファイルを使用してローカライズ設定を構成できます。

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>SQLSRV ドライバーを使用してロケール情報を設定する  
php.ini ファイルの最後に、次を追加します。
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>PDO_SQLSRV ドライバーを使用してロケール情報を設定する  
php.ini ファイルの最後に、次を追加します。
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
**オプション**は次の値のいずれかです。  
  
|オプション|動作の説明|
|---------|---------------|
|0|ドライバーでは、システム ロケール設定が無視されます。|
|1|ドライバーによって LC_CTYPE 変数が読み取られます。|
|2|ドライバーによって LC_ALL 変数が読み取られます (これが既定値です)。|
  

`LC_CTYPE` カテゴリによって、テキスト データ文字のバイト シーケンスの解釈、文字の分類、および文字クラスの動作を制御する文字処理ルールが決まります。 これで大文字、小文字、英字、英字以外の文字などの認識が制御されます。

### <a name="explanation"></a>説明

1. オプション 0 -- アプリケーション ロケールを変更しない場合にこれを使用します。

1. オプション 1 -- これを使用すると、他の `LC_xxx` カテゴリに影響を与えずに、`LC_CTYPE` のシステム値のみが設定されます。

1. オプション 2 -- `LC_ALL` を使用すると、すべての `LC_xxx` カテゴリがオーバーライドされ、php アプリケーションとその拡張機能に影響が及びます。

php スクリプトのロケールがシステムのロケールと同じでない場合は、php 組み込み関数 [setlocale](https://www.php.net/manual/en/function.setlocale.php) を呼び出して、php スクリプトでロケールを指定する必要があります。 

たとえば、システムの既定値が `en_US.UTF-8` で、php スクリプトで `de_DE.UTF-8` が使用されている場合は、php 関数 `setlocale()` を適切に呼び出します。

オプション 2 の場合、`LC_ALL` 変数とは異なる場合にのみ、php スクリプトで目的のロケールを指定します。

> [!NOTE]
> php.ini に何も定義されていない場合、現在の既定では、`LC_ALL` に基づいて他のすべてのロケール設定がオーバーライドされます。これは**非推奨**になります。 近い将来、既定ではシステム ロケール設定が無視されます。 そのため、現在の動作を維持する場合は、そのために php.ini ファイルを変更する必要があります。

sqlsrv と pdo_sqlsrv の両方のドライバーが有効な場合、2 つのドライバーに異なるオプションを設定することはお勧めしません。
