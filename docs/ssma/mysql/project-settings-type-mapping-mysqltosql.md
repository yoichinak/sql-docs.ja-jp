---
description: プロジェクトの設定 (型のマッピング) (MySQLToSQL)
title: プロジェクトの設定 (型のマッピング) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a6f4bc99caceeb7011c932c86e636304941c459c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418488"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>プロジェクトの設定 (型のマッピング) (MySQLToSQL)
型マッピングプロジェクトの設定を使用すると、SSMA プロジェクトの既定の型マッピングを設定できます。  

型マッピングは、[プロジェクトの設定] ダイアログボックスと [既定のプロジェクトの設定] ダイアログボックスで使用できます。  
  
-   [プロジェクトの設定] ダイアログボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 型マッピングの設定にアクセスするには、[ツール] メニューの [プロジェクトの設定] をクリックし、左ペインの [型マッピング] をクリックします。  
  
-   [既定のプロジェクトの設定] ダイアログボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 型マッピングの設定にアクセスするには、[ツール] メニューの [既定のプロジェクト設定] をクリックし、[移行 **先のバージョン** ] ドロップダウンから表示/変更が必要な設定を選択して、左側のウィンドウの [種類のマッピング] をクリックします。  
  
## <a name="options"></a>オプション  
  
##### <a name="source-type"></a>ソースの種類  
これは MySQL データ型で、ターゲットデータベースのデータ型にマップする必要があります。  
  
##### <a name="target-type"></a>ターゲットの種類  
指定された MySQL データ型のターゲットデータベースデータ型。  
  
##### <a name="add"></a>追加  
[マッピング] ボックスの一覧にデータ型を追加する場合にクリックします。  
  
##### <a name="edit"></a>編集  
[マッピング] ボックスの一覧で選択したデータ型を編集する場合にクリックします。  
  
##### <a name="remove"></a>[削除]  
クリックすると、選択したデータ型マッピングが [マッピング] ボックスの一覧から削除されます。  
  
##### <a name="reset-to-default"></a>[既定値にリセット]  
クリックすると、[型マッピング] の一覧が SSMA の既定値にリセットされます。  
  
## <a name="type-mappings"></a>型のマッピング  
次の表は、ソースとターゲットのデータ型の既定のマッピングを示しています。  
  
|MySQL データ型|SQL Server データ型|  
|-|-|  
|bigint|bigint|  
|bigint [*..255]|bigint|  
|binary|バイナリ [1]|  
|binary [0 ..1]|バイナリ [1]|  
|バイナリ [2.. 255]|バイナリ [*]|  
|bit|バイナリ [1]|  
|ビット [0.. 8]|バイナリ [1]|  
|bit [17.. 24]|バイナリ [3]|  
|bit [25.. 32]|バイナリ [4]|  
|bit [33.. 40]|バイナリ [5]|  
|bit [41.. 48]|バイナリ [6]|  
|bit [49.. 56]|バイナリ [7]|  
|bit [57.. 64]|バイナリ [8]|  
|bit [9.. 16]|バイナリ [2]|  
|blob (blob)|varbinary(max)|  
|blob [0 ..1]|varbinary [1]|  
|blob [2.. 8000]|varbinary [*]|  
|blob [8001.. *]|varbinary(max)|  
|[bool]|bit|  
|boolean|bit|  
|char|nchar [1]|  
|char byte|バイナリ [1]|  
|char byte [0 ..1]|バイナリ [1]|  
|char byte [2.. 255]|バイナリ [*]|  
|char [0 ..1]|nchar [1]|  
|char [2.. 255]|nchar [*]|  
|character|nchar [1]|  
|文字の変化 [0 ..1]|nvarchar [1]|  
|文字の変化 [2.. 255]|nvarchar|  
|文字 [0 ..1]|nchar [1]|  
|文字 [2.. 255]|nchar [*]|  
|date|date|  
|DATETIME|datetime2 [0]|  
|dec|decimal|  
|dec [*..65]|decimal [*] [0]|  
|dec [*..65] [ \* ..?|decimal [*] [ \* ]|  
|decimal|decimal|  
|decimal [*..65]|decimal [*] [0]|  
|decimal [*..65] [ \* ..?|decimal [*] [ \* ]|  
|double|float [53]|  
|double precision|float [53]|  
|倍精度浮動小数点型 [*..255] [ \* ..?|数値 [*] [ \* ]|  
|double [*..255] [ \* ..?|数値 [*] [ \* ]|  
|固定|numeric|  
|修正済み [*..65] [ \* ..?|数値 [*] [ \* ]|  
|float|float [24]|  
|float [*..255] [ \* ..?|数値 [*] [ \* ]|  
|float [*..53]|float [53]|  
|INT|INT|  
|int [*..255]|INT|  
|整数 (integer)|INT|  
|integer [*..255]|INT|  
|longblob|varbinary(max)|  
|longtext|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|INT|  
|mediumint[*..255]|INT|  
|mediumtext|nvarchar(max)|  
|national char|nchar [1]|  
|national char [0 ..1]|nchar [1]|  
|national char [2.. 255]|nchar [*]|  
|national character|nchar [1]|  
|各国語文字の変化|nvarchar [1]|  
|各国語文字のさまざまな [0 ..1]|nvarchar [1]|  
|国別文字 [2.. 4000]|nvarchar [*]|  
|各国語文字のさまざまな [4001.. *]|nvarchar(max)|  
|national character [0 ..1]|nchar [1]|  
|national character [2.. 255]|nchar [*]|  
|national varchar|nvarchar [1]|  
|national varchar [0 ..1]|nvarchar [1]|  
|national varchar [2.. 4000]|nvarchar [*]|  
|national varchar [4001.. *]|nvarchar(max)|  
|nchar|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0 ..1]|nvarchar [1]|  
|nchar varchar [2.. 4000]|nvarchar [*]|  
|nchar varchar [4001.. *]|nvarchar(max)|  
|nchar [0 ..1]|nchar [1]|  
|nchar [2.. 255]|nchar [*]|  
|numeric|numeric|  
|数値 [*..65]|数値 [*] [0]|  
|数値 [*..65] [ \* ..?|数値 [*] [ \* ]|  
|nvarchar|nvarchar [1]|  
|nvarchar [0 ..1]|nvarchar [1]|  
|nvarchar [2.. 4000]|nvarchar [*]|  
|nvarchar [4001.. *]|nvarchar(max)|  
|real|float [53]|  
|real [*..255] [ \* ..?|数値 [*] [ \* ]|  
|serial|bigint|  
|smallint|smallint|  
|smallint [*..255]|smallint|  
|text|nvarchar(max)|  
|テキスト [0 ..1]|nvarchar [1]|  
|テキスト [2.. 4000]|nvarchar [*]|  
|テキスト [4001.. *]|nvarchar(max)|  
|time|time|  
|timestamp|DATETIME|  
|tinyblob|varbinary [255]|  
|tinyint|smallint|  
|tinyint [*..255]|smallint|  
|tinytext|nvarchar [255]|  
|符号なし bigint|bigint|  
|符号なし bigint [*..255]|bigint|  
|unsigned dec|decimal|  
|unsigned dec [*..65]|decimal [*] [0]|  
|unsigned dec [*..65] [ \* ..?|decimal [*] [ \* ]|  
|符号なし10進|decimal|  
|符号なし10進数 [*..65]|decimal [*] [0]|  
|符号なし10進数 [*..65] [ \* ..?|decimal [*] [ \* ]|  
|符号なし double|float [53]|  
|符号なし倍精度|float [53]|  
|符号なし倍精度 [*..255] [ \* ..?|数値 [*] [ \* ]|  
|unsigned double [*..255] [ \* ..?|数値 [*] [ \* ]|  
|unsigned fixed|numeric|  
|unsigned fixed [*..65] [ \* ..?|数値 [*] [ \* ]|  
|unsigned float|float [24]|  
|unsigned float [*..255] [ \* ..?|数値 [*] [ \* ]|  
|unsigned float [*..53]|float [53]|  
|unsigned int|bigint|  
|unsigned int [*..255]|bigint|  
|符号なし整数|bigint|  
|符号なし整数 [*..255]|bigint|  
|署名されていない mediumint|INT|  
|署名されていない mediumint [*..255]|INT|  
|符号なし数値|numeric|  
|符号なし数値 [*..65]|数値 [*] [0]|  
|符号なし数値 [*..65] [ \* ..?|数値 [*] [ \* ]|  
|符号なし実数|float [53]|  
|unsigned real [*..255 [[ \* ..?|数値 [*] [ \* ]|  
|unsigned smallint|INT|  
|unsigned smallint [*..255]|INT|  
|unsigned tinyint|tinyint|  
|unsigned tinyint [*..255]|tinyint|  
|varbinary [0 ..1]|varbinary [1]|  
|varbinary [2.. 8000]|varbinary [*]|  
|varbinary [8001.. *]|varbinary(max)|  
|varchar [0 ..1]|nvarchar [1]|  
|varchar [2.. 4000]|nvarchar [*]|  
|varchar [4001.. *]|nvarchar(max)|  
|year|smallint|  
|年 [2.. 2]|smallint|  
|年 [4.. 4]|smallint|  
  
##### <a name="add"></a>追加  
[マッピング] ボックスの一覧にデータ型を追加する場合にクリックします。  
  
##### <a name="edit"></a>編集  
[マッピング] ボックスの一覧でデータ型を編集する場合にクリックします。  
  
##### <a name="remove"></a>[削除]  
クリックすると、選択したデータ型マッピングが [マッピング] ボックスの一覧から削除されます。  
  
##### <a name="reset-to-default"></a>[既定値にリセット]  
すべてのデータ型マッピングを SSMA の既定値にリセットする場合にクリックします。  
  
