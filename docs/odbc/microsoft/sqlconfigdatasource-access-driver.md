---
description: SQLConfigDataSource (Access ドライバー)
title: SQLConfigDataSource (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411988"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 データソースを動的に追加、変更、または削除するために使用される **Sqlconfigdatasource** 関数は、次のキーワードを動的に使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|組み合わせの順序|フィールドの並べ替え順序。<br /><br /> これにより、[セットアップ] ダイアログボックスの **照合順序** と同じオプションが設定されます。|  
|COMPACT_DB|データベースファイルに対してデータ圧縮を実行します。 の形式は次のとおりです。 COMPACT_DB =<path_name><optionaL_sort_order>\<optional ENCRYPT keyword> 。<br /><br /> DSN キーワードと同じステートメントで COMPACT_DB キーワードを使用すると、このドライバーは DSN キーワードを無視します。 そのため、データベースを圧縮し、DSN を指定するには、2段階のプロセスを実行します。|  
|CREATE_DB|データベースファイルを作成します。 の形式は次のとおりです。 CREATE_DB =<path_name>\<optional_sort-order><optional_ENCRYPT キーワード>。ここで、パス名は Microsoft access データベースへの完全なパスです。 パス名に既存のデータベースが指定されている場合は、エラーが返されます。 並べ替え順序は、[Microsoft Access のセットアップ] ダイアログボックスで [作成] ボタンをクリックしたときに表示される [新しいデータベース] ダイアログボックスで設定したものになります。 並べ替え順序が指定されていない場合は、General が使用されます。<br /><br /> DSN キーワードと同じステートメントで CREATE_DB キーワードを使用すると、このドライバーは DSN キーワードを無視します。 そのため、データベースを作成し、DSN を指定するには、2段階のプロセスを実行します。CREATE_DB キーワードを使用する場合、作成する Microsoft Access データベースのパス名に1つ以上のスペースが含まれている場合は、次の例に示すように、パス名全体を二重引用符で囲む必要があります。<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (引用符は不要)|  
|CREATE_SYSDB|システムデータベースファイルを作成します。 の形式は次のとおりです。 CREATE_SYSDB =。 \<path-name> \<optional-sort-order> パス名は、Microsoft access データベースへの完全なパスです。 パス名に既存のデータベースが指定されている場合は、エラーが返されます。 並べ替え順序は、[ **ODBC Microsoft Access セットアップ**] ダイアログボックスで [**作成**] ボタンをクリックしたときに表示される [**新しいデータベース**] ダイアログボックスで設定されます。 並べ替え順序が指定されていない場合は、General が使用されます。|  
|CREATE_V2DB|Microsoft Access 2.0 と互換性のあるデータベースファイルを作成します。 の形式は次のとおりです。 CREATE_V2DB =。 \<path-name> \<optional-sort-order> パス名は、Microsoft access データベースへの完全なパスです。 パス名に既存のデータベースが指定されている場合は、エラーが返されます。 並べ替え順序は、[Microsoft Access のセットアップ] ダイアログボックスで [作成] ボタンをクリックしたときに表示される [新しいデータベース] ダイアログボックスで設定したものになります。 並べ替え順序が指定されていない場合は、General が使用されます。<br /><br /> DSN キーワードと同じステートメントで CREATE_V2DB キーワードを使用すると、このドライバーは DSN キーワードを無視します。 そのため、データベースを作成し、DSN を指定するには、2段階のプロセスを実行します。<br /><br /> CREATE_V2DB キーワードを使用する場合、作成する Microsoft Access データベースのパス名に1つ以上のスペースが含まれている場合は、次の例に示すように、パス名全体を二重引用符で囲む必要があります。<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (引用符は不要)|  
|DBQ|データベースファイルの名前です。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **データベース** ] と同じオプションが設定されます。|  
|DEFAULTDIR|データベースファイルへのパスの指定。|  
|Description|データソース内のデータの説明。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **説明** ] と同じオプションが設定されます。|  
|DRIVER|ドライバー DLL へのパス指定。|  
|DRIVERID|ドライバーの整数 ID。  25 (Microsoft Access)|  
|FIL|Microsoft Access 用のファイルの種類 MS Access|  
|IMPLICITCOMMITSYNC|Microsoft Access ドライバーが内部コミットまたは暗黙的コミットを非同期的に実行するかどうかを決定します。 この値は、最初は "Yes" に設定されます。これは、Microsoft Access ドライバーが内部/暗黙のトランザクションのコミットが完了するまで待機することを意味します。<br /><br /> このオプションの値は、結果を慎重に考慮することなく変更しないでください。 オプションの詳細については、 *『 Microsoft Jet データベースエンジンプログラマーズガイド』* を参照してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **ImplicitCommitSync** ] と同じオプションが設定されます。|  
|MAXBUFFERSIZE|ディスクとの間でデータを転送するために Microsoft Access によって使用される内部バッファーのサイズ (kb 単位)。 既定のバッファーサイズは 2048 KB (2048 と表示されます) です。 256で割り切れる整数値を使用できます。 これにより、[セットアップ] ダイアログボックスの [ **バッファーサイズ** ] と同じオプションが設定されます。|  
|MAXSCANROWS|既存のデータに基づいて列のデータ型を設定するときにスキャンされる行の数。<br /><br /> スキャンする行には、1 ~ 16 の数値を入力できます。 既定値は8です。0に設定されている場合は、すべての行がスキャンされます。 (制限外の数値はエラーを返します)。<br /><br /> これにより、[セットアップ] ダイアログボックスで **スキャンする行** と同じオプションが設定されます。|  
|PAGETIMEOUT|ページ (使用されていない場合) が削除される前にバッファーに残っている時間をミリ秒単位で指定します。 既定値は5秒 (0.5 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されることに注意してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **ページタイムアウト** ] と同じオプションが設定されます。|  
|PWD|パスワード。|  
|READONLY|ファイルを読み取り専用にする場合は TRUE。ファイルが読み取り専用でないようにする場合は FALSE。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **読み取り専用** ] と同じオプションが設定されます。|  
|REPAIR_DB|コミット処理中に発生したエラーによって破損したデータベースを修復します。<br /><br /> DSN キーワードと同じステートメントで REPAIR_DB キーワードを使用すると、このドライバーは DSN キーワードを無視します。 そのため、データベースを修復し、DSN を指定するには、2段階のプロセスを実行します。|  
|SYSTEMDB|Microsoft Access ドライバーの場合は、システムデータベースファイルのパスを指定します。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **システムデータベース** ] と同じオプションが設定されます。|  
|レッド|エンジンが使用するバックグラウンドスレッドの数。 この値は既定で3に設定されていますが、変更することができます。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **スレッド** ] と同じオプションが設定されます。|  
|UID|Microsoft Access ドライバーの場合、ログインに使用されるユーザー ID 名。|  
|USERCOMMITSYNC|Microsoft Access ドライバーがユーザー定義のトランザクションを非同期的に実行するかどうかを決定します。 この値は、最初は "Yes" に設定されます。これは、ユーザー定義トランザクションのコミットが完了するまで Microsoft Access ドライバーが待機することを意味します。<br /><br /> このオプションの値は、結果を慎重に考慮することなく変更しないでください。 オプションの詳細については、 *『 Microsoft Jet データベースエンジンプログラマーズガイド』* を参照してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **Usercommitsync** ] と同じオプションが設定されます。|
