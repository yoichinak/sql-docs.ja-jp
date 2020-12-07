---
description: SQLConfigDataSource (テキスト ファイル ドライバー)
title: SQLConfigDataSource (テキストファイルドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 400b83d382140d4661b103e24449f14ecdfda43d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411868"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキストファイルドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 データソースを動的に追加、変更、または削除するために使用される **Sqlconfigdatasource** 関数は、次のキーワードを動的に使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|CHARACTERSET|テキストドライバーの場合は、OEM または ANSI。|  
|COLNAMEHEADER|テキストドライバーの場合、データの最初のレコードで列名を指定するかどうかを示します。 TRUE または FALSE のいずれかです。|  
|DEFAULTDIR|ディレクトリへのパス指定。|  
|Description|データソース内のデータの説明。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **説明** ] と同じオプションが設定されます。|  
|DRIVER|ドライバー DLL へのパス指定。|  
|DRIVERID|ドライバーの整数 ID。 27 (テキスト)|  
|補助|データソース上のテキストファイルのファイル名拡張子を一覧表示します。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **拡張機能** ] の一覧と同じオプションが設定されます。|  
|FIL|ファイルの種類のテキスト|  
|FILETYPE|テキストドライバー (テキスト) のファイルの種類。|  
|FORMAT|テキストドライバーの場合、には、FIXEDLENGTH、TABDELIMITED れた、CSVDELIMITED (コンマ)、または区切り記号 () (かっこで指定された特殊文字) を指定できます。 特殊文字は、1文字の長さで、文字、10進数、または16進数形式で指定できます。|  
|MAXSCANROWS|既存のデータに基づいて列のデータ型を設定するときにスキャンされる行の数。<br /><br /> テキストドライバーについては、スキャンする行の数として 1 ~ 32767 の数値を入力できます。ただし、この値は常に既定で25に設定されます。 (制限外の数値はエラーを返します)。<br /><br /> これにより、[セットアップ] ダイアログボックスで **スキャンする行** と同じオプションが設定されます。|  
|READONLY|ファイルを読み取り専用にする場合は TRUE。ファイルが読み取り専用でないようにする場合は FALSE。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **読み取り専用** ] と同じオプションが設定されます。|
