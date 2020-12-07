---
description: プログラムで Access ドライバーのオプションの設定
title: Access Driver | のプログラムでオプションを設定するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ae798b3c3d91917e461bb6b5a58cb06734870d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412418"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>プログラムで Access ドライバーのオプションの設定

|オプション|説明|認証方法|  
|------------|-----------------|------------|  
|バッファー サイズ|ディスクとの間でデータを転送するために Microsoft Access によって使用される内部バッファーのサイズ (kb 単位)。 既定のバッファーサイズは 2048 KB (2048 と表示されます) です。 256で割り切れる整数値を入力できます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで MAXBUFFERSIZE キーワードを使用します。|  
|データ ソース名|給与や職員など、データソースを識別する名前。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**DSN**キーワードを使用します。|  
|データベース|Microsoft Access データソースは、データベースを選択または作成せずに設定できます。 セットアップ時にデータベースが指定されていない場合、データソースへの接続時にデータベースファイルを選択するように求めるメッセージがユーザーに表示されます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**dbq**キーワードを使用します。|  
|説明|データソース内のデータの説明 (省略可能)。たとえば、"入社日、給与履歴、およびすべての従業員の現在のレビュー" などです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**DESCRIPTION**キーワードを使用します。|  
|排他的|[ **排他** ] ボックスが選択されている場合、データベースは排他モードで開き、一度に1人のユーザーのみがアクセスできます。 排他モードで実行すると、パフォーマンスが向上します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**EXCLUSIVE**キーワードを使用します。|  
|ImplicitCommitSync|トランザクションの外部で行われた変更がデータベースに書き込まれる方法を決定します。 この値は、最初は "Yes" に設定されます。これは、Microsoft Access ドライバーが内部/暗黙のトランザクションのコミットが完了するまで待機することを意味します。|このオプションは、Microsoft Access ドライバーの **[詳細オプションの設定** ] ダイアログボックスに含まれています。|  
|ページタイムアウト|ページ (使用されていない場合) が削除される前にバッファーに残っている時間をミリ秒単位で指定します。 Microsoft Access ドライバーの場合、既定値は500ミリ秒 (0.5 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されます。<br /><br /> 固有の遅延が発生したため、ページタイムアウトを0にすることはできません。 ページタイムアウトオプションがその値より下に設定されている場合でも、ページタイムアウトを固有の遅延より小さくすることはできません。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**PAGETIMEOUT**キーワードを使用します。|  
|[読み取り専用]|データベースを読み取り専用として指定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**READONLY**キーワードを使用します。|  
|システムデータベース|アクセスする Microsoft access データベースで使用する Microsoft Access システムデータベースの完全なパス。<br /><br /> [ **システムデータベース** ] をクリックして、使用するシステムデータベースを選択します。 ODBC Microsoft Access driver は、ユーザーに名前とパスワードの入力を求めます。 既定の名前は Admin で、管理者ユーザーの Microsoft Access の既定のパスワードは空の文字列です。<br /><br /> Microsoft Access データベースのセキュリティを強化するには、管理者ユーザーを置き換える新しいユーザーを作成し、管理者ユーザーを削除するか、管理者ユーザーがアクセスできるオブジェクトを変更します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**systemdb**キーワードを使用します。|  
|Threads|エンジンが使用するバックグラウンドスレッドの数。 Microsoft Access ドライバーでは、この値は既定で3に設定されていますが、変更することができます。 ユーザーは、データベースに大量のアクティビティがある場合にスレッド数を増やすことができます。<br /><br /> このオプションは、Microsoft Access ドライバーの **[詳細オプションの設定** ] ダイアログボックスに含まれています。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)への呼び出しで**THREADS**キーワードを使用します。|  
|UserCommitSync|Microsoft Access ドライバーが明示的にユーザー定義のトランザクションを非同期的に実行するかどうかを決定します。 この値は、最初は "Yes" に設定されます。これは、ユーザー定義トランザクションのコミットが完了するまで Microsoft Access ドライバーが待機することを意味します。<br /><br /> このオプションを [False] に設定すると、マルチユーザー環境で予期しない結果が生じる可能性があります。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)の呼び出しで**usercommitsync**キーワードを使用します。|
