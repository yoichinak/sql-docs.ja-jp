---
description: インストーラー DLL 関数の概要
title: インストーラー DLL 関数の概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3666808659abb29a1f5a1eb1e8be62e8cf0507f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461234"
---
# <a name="installer-dll-function-summary"></a>インストーラー DLL 関数の概要
インストーラー DLL の関数を次の表に示します。 各関数の構文とセマンティクスの詳細については、「 [インストーラー DLL API リファレンス](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)」を参照してください。  
  
|タスク|関数名|目的|  
|----------|-------------------|-------------|  
|ODBC のインストール|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|ドライバー固有のセットアップ DLL を読み込みます。|  
||[Sqlgetdrivers ドライバー](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|インストールされているドライバーの一覧を返します。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|システム情報にドライバーを追加します。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|ドライバーマネージャーのターゲットディレクトリを返します。|  
||[Sqlインストーラエラー](../../../odbc/reference/syntax/sqlinstallererror-function.md)|インストーラー関数のエラーまたは状態の情報を返します。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|システム情報に変換プログラムを追加します。|  
||[Sqlpostインストーラエラー](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|ドライバーまたはトランスレーターセットアップライブラリがエラーを報告できるようにします。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|システム情報からドライバーを削除します。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|システム情報から ODBC コアコンポーネントを削除します。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|システム情報から変換プログラムを削除します。|  
|データ ソースの構成|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|ドライバー固有のセットアップ DLL を呼び出します。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|データソースを追加するためのダイアログボックスを表示します。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|DSN 値を一覧表示する Odbc.ini エントリのシステム情報内の場所を示す構成モードを取得します。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|システム情報に値を書き込みます。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|変換プログラムを選択するためのダイアログボックスを表示します。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|データソースとドライバーを構成するためのダイアログボックスを表示します。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|ファイル Dsn から情報を読み取ります。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|既定のデータソースを削除します。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|データソースを削除します。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|DSN 値を一覧表示する Odbc.ini エントリのシステム情報の場所を示す構成モードを設定します。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|データソース名の長さと有効性をチェックします。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|データソースを追加します。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|ファイル Dsn に情報を書き込みます。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|システム情報から値を取得します。|
