---
description: SQLConfigDataSource (Paradox ドライバー)
title: SQLConfigDataSource (Paradox ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ced7a482f79426961e8532cd343691b3f023703c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411938"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox ドライバー)
> [!NOTE]  
>  このトピックでは、Paradox ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 データソースを動的に追加、変更、または削除するために使用される **Sqlconfigdatasource** 関数は、次のキーワードを動的に使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|組み合わせの順序|フィールドの並べ替え順序。<br /><br /> Paradox ドライバーを使用する場合、シーケンスは ASCII (既定)、国際対応、スウェーデン語 (フィンランド)、またはノルウェー語 (デンマーク) にすることができます。<br /><br /> これにより、[セットアップ] ダイアログボックスの **照合順序** と同じオプションが設定されます。|  
|DBQ|データベースファイルの名前です。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **データベース** ] と同じオプションが設定されます。|  
|DEFAULTDIR|ディレクトリへのパス指定。|  
|Description|データソース内のデータの説明。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **説明** ] と同じオプションが設定されます。|  
|DRIVER|ドライバー DLL へのパス指定。|  
|DRIVERID|ドライバーの整数 ID。<br /><br /> 26 (Paradox 3 .x)<br /><br /> 282 (Paradox 4.x)<br /><br /> 538 (Paradox 5.x)|  
|外税|データベースを排他モードで開くか (一度に1人のユーザーのみがアクセスする)、共有モードにするかを決定します (複数のユーザーが同時にアクセスします)。 True (排他モード) または false (共有モード) を指定できます。<br /><br /> これにより、[セットアップ] ダイアログボックスで [ **排他** ] と同じオプションが設定されます。|  
|FIL|ファイルの種類 Paradox 3. x、Paradox 4.x、または Paradox 5.x|  
|FILETYPE|テキストドライバー (テキスト) のファイルの種類。|  
|PAGETIMEOUT|ページ (使用されていない場合) が削除される前にバッファーに残ったままになる時間を秒単位で指定します。 既定値は 600 1/10 (60 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されることに注意してください。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **ページタイムアウト** ] と同じオプションが設定されます。|  
|PARADOXNETPATH|PDOXUSRS.net ファイル (Paradox 4) が含まれているため、Paradox ロックデータベースを含むディレクトリの完全パスです。*x*) または PARADOX.net ファイル (PARADOX 5)。*x*)。 ディレクトリにこれらのファイルのいずれかが含まれていない場合は、Paradox ドライバーによって作成されます。 これらのファイルの詳細については、「Paradox のドキュメント」を参照してください。<br /><br /> ネットワークディレクトリを選択する前に、Paradox ユーザー名を入力する必要があります。<br /><br /> これにより、[セットアップ] ダイアログボックスの **[ネットワークディレクトリの選択** ] と同じオプションが設定されます。|  
|PARADOXNETSTYLE|Paradox ドライバーの場合、paradox データへのアクセス時に使用するネットワークアクセススタイル (Paradox 3 の場合は "3.x")。Paradox 4 の場合は*x* または "4.x"。*x* または5。*x*。 バージョンが Paradox 4 の場合は、"3. x" または "4.x" に設定できます。*x* または5。*x*;バージョンが Paradox 3 の場合。*x*の場合、スタイルは "3.x" である必要があります。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **Net Style** ] と同じオプションが設定されます。|  
|PARADOXUSERNAME|Paradox ドライバーの場合は、Paradox ユーザー名です。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **ユーザー名** ] と同じオプションが設定されます。|  
|PWD|パスワード。<br /><br /> これは省略可能なキーワードで、ドライバーによってファイルに書き込まれることはありません。 これは、パスワードで保護された Paradox ファイルに対する **SQLDriverConnect** の呼び出しで使用されます。 使用されるパスワードは、テーブルが開かれるたびに有効になります。 接続文字列にパスワードが渡されない場合、そのテーブルのパスワードは設定されません。 テーブルのパスワードが異なる場合は、複数のテーブルを同じセッションで開くことも、テーブルを結合することもできません。|  
|READONLY|ファイルを読み取り専用にする場合は TRUE。ファイルが読み取り専用でないようにする場合は FALSE。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **読み取り専用** ] と同じオプションが設定されます。|  
|レッド|エンジンが使用するバックグラウンドスレッドの数。 この値は3であり、変更することはできません。<br /><br /> これにより、[セットアップ] ダイアログボックスの [ **スレッド** ] と同じオプションが設定されます。|
