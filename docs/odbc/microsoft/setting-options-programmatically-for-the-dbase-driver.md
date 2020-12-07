---
description: dBASE ドライバーのプログラムでオプションの設定
title: DBASE ドライバーのプログラムを使用したオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4b86b8284ca9a47e3ad40b1680a362035a3f13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471584"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>dBASE ドライバーのプログラムでオプションの設定

|オプション|説明|認証方法|  
|------------|-----------------|------------|  
|おおよその行数|テーブルサイズの統計を近似するかどうかを決定します。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**STATISTICS**キーワードを使用します。|  
|照合順序|フィールドの並べ替え順序。<br /><br /> このシーケンスには、ASCII (既定値) と国際対応のいずれかを指定できます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)の呼び出しで、**組み合わせて sequence**キーワードを使用します。|  
|データ ソース名|給与や職員など、データソースを識別する名前。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**DSN**キーワードを使用します。|  
|データベース|Microsoft Access データソースは、データベースを選択または作成せずに設定できます。 セットアップ時にデータベースが提供されない場合、ユーザーは、データソースに接続するときにデータベースファイルを選択するように求められます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**dbq**キーワードを使用します。|  
|説明|データソース内のデータの説明 (省略可能)。たとえば、"入社日、給与履歴、およびすべての従業員の現在のレビュー" などです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**DESCRIPTION**キーワードを使用します。|  
|排他的|[ **排他** ] ボックスが選択されている場合、データベースは排他モードで開き、一度に1人のユーザーのみがアクセスできます。 排他モードで実行すると、パフォーマンスが向上します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**EXCLUSIVE**キーワードを使用します。|  
|ページタイムアウト|ページ (使用されていない場合) がバッファーに残っている場合に、削除されるまでの時間を秒単位で指定します。 既定値は 600 1/10 (60 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されます。<br /><br /> 固有の遅延が発生したため、ページタイムアウトを0にすることはできません。 ページタイムアウトオプションがその値より下に設定されている場合でも、ページタイムアウトを固有の遅延より小さくすることはできません。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**PAGETIMEOUT**キーワードを使用します。|  
|[読み取り専用]|データベースを読み取り専用として指定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**READONLY**キーワードを使用します。|  
|ディレクトリの選択|アクセスするファイルが格納されているディレクトリを選択できるダイアログボックスが表示されます。<br /><br /> データソースディレクトリを定義するときは、最も頻繁に使用されるファイルが置かれているディレクトリを指定します。 ODBC ドライバーでは、このディレクトリが既定のディレクトリとして使用されます。 頻繁に使用する場合は、他のファイルをこのディレクトリにコピーします。 または、次のようにディレクトリ名を指定して、SELECT ステートメント内のファイル名を修飾することもできます。<br /><br /> \*C:\MYDIR\EMP から選択<br /><br /> または、 **SQLSetConnectOption** 関数を SQL_CURRENT_QUALIFIER オプションと共に使用して、新しい既定のディレクトリを指定することもできます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|  
|削除された行の表示|削除済みとしてマークされている行を取得または配置できるかどうかを指定します。 オフにした場合、削除された行は表示されません。選択した場合、削除された行は、削除されていない行と同じように扱われます。 既定値はオフです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)の呼び出しで**DELETED**キーワードを使用します。|
