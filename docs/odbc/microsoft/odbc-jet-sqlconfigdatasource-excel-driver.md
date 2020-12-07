---
description: ODBC Jet SQLConfigDataSource (Excel ドライバー)
title: ODBC Jet SQLConfigDataSource (Excel Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61fcc1e7df00f14a7b92e294262b7806382a3d52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500305"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 データソースを動的に追加、変更、または削除するために使用される **Sqlconfigdatasource** 関数は、次のキーワードを動的に使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|DBQ|Microsoft excel driver For microsoft Excel 5.0 以降のファイルにアクセスする場合は、ブックファイルの名前。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **データベース** ] と同じオプションが設定されます。|  
|DEFAULTDIR|ディレクトリへのパス指定。<br /><br /> これにより、 **[ディレクトリの選択** ] または [セットアップ] ダイアログボックスの **[ブックの選択** ] と同じオプションが設定されます。|  
|Description|データソース内のデータの説明。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **説明** ] と同じオプションが設定されます。|  
|DRIVER|ドライバー DLL へのパス指定。|  
|DRIVERID|ドライバーの整数 ID。<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|ファイルの種類。たとえば、Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000、Excel 2003 などです。|  
|FIRSTROWHASNAMES|範囲の最初の行のセルにテーブルの列名が含まれるかどうかを示します (1)。それ以外の場合は (0)。|  
|MAXSCANROWS|既存のデータに基づいて列のデータ型を設定するときにスキャンされる行の数。<br /><br /> スキャンする行には、1 ~ 16 の数値を入力できます。 既定値は8です。0に設定されている場合は、すべての行がスキャンされます。 (制限外の数値はエラーを返します)。<br /><br /> これにより、[セットアップ] ダイアログボックスで **スキャンする行** と同じオプションが設定されます。|  
|READONLY|ファイルを読み取り専用にする場合は TRUE。ファイルが読み取り専用でないようにする場合は FALSE。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **読み取り専用** ] と同じオプションが設定されます。|  
|レッド|エンジンが使用するバックグラウンドスレッドの数。 Microsoft Access ドライバーでは、この値は既定で3に設定されていますが、変更することができます。 DBASE の場合、MicrosoftExceldriver の値は3であり、変更することはできません。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **スレッド** ] と同じオプションが設定されます。|
