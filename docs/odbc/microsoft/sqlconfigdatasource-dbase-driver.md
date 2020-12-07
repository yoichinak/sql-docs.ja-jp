---
description: SQLConfigDataSource (dBASE ドライバー)
title: SQLConfigDataSource (dBASE ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23e734c5aafc903e210eea18f002f4c5e8d7a456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411958"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE ドライバー)
> [!NOTE]  
>  このトピックでは、dBASE ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 データソースを動的に追加、変更、または削除するために使用される **Sqlconfigdatasource** 関数は、次のキーワードを動的に使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|組み合わせの順序|フィールドの並べ替え順序。<br /><br /> このシーケンスには、ASCII (既定値) と国際対応のいずれかを指定できます。<br /><br /> これにより、[セットアップ] ダイアログボックスの **照合順序** と同じオプションが設定されます。|  
|DEFAULTDIR|ディレクトリへのパス指定。|  
|DELETED|DBASE ドライバーの場合は、削除済みとしてマークされている行を取得または配置できるかどうかを指定します。 1に設定すると、削除された行は表示されません。0に設定すると、削除された行は削除されていない行と同じように扱われます。<br /><br /> これにより、[セットアップ] ダイアログボックスに [ **削除された行を表示する** ] と同じオプションが設定されます。|  
|Description|データソース内のデータの説明。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **説明** ] と同じオプションが設定されます。|  
|DRIVER|ドライバー DLL へのパス指定。|  
|DRIVERID|ドライバーの整数 ID。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|ファイルの種類 dBase III、dBase IV、または dBase 5|  
|PAGETIMEOUT|ページ (使用されていない場合) が削除される前にバッファーに残ったままになる時間を秒単位で指定します。 既定値は 600 1/10 (60 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されることに注意してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **ページタイムアウト** ] と同じオプションが設定されます。|  
|READONLY|ファイルを読み取り専用にする場合は TRUE。ファイルが読み取り専用でないようにする場合は FALSE。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **読み取り専用** ] と同じオプションが設定されます。|  
|STATISTICS|DBASE ドライバーの場合、テーブルサイズの統計を近似するかどうかを決定します。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されることに注意してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **おおよその行数** ] と同じオプションが設定されます。|  
|レッド|エンジンが使用するバックグラウンドスレッドの数。 この値は3であり、変更することはできません。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **スレッド** ] と同じオプションが設定されます。|
