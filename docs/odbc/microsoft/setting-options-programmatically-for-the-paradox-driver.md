---
description: Paradox ドライバーのプログラムでオプションの設定
title: Paradox ドライバーのプログラムによるオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 85b63df9e18b835c96bc0e59f7c937ece69f3999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471574"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Paradox ドライバーのプログラムでオプションの設定

|オプション|説明|認証方法|  
|------------|-----------------|------------|  
|ディレクトリ|ターゲットディレクトリを設定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|  
|照合順序|フィールドの並べ替え順序。<br /><br /> シーケンスには、ASCII (既定値)、国際対応、スウェーデン語 (フィンランド)、またはノルウェー語 (デンマーク) を指定できます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)の呼び出しで、**組み合わせて sequence**キーワードを使用します。|  
|説明|データソース内のデータの説明 (省略可能)。たとえば、"入社日、給与履歴、およびすべての従業員の現在のレビュー" などです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**DESCRIPTION**キーワードを使用します。|  
|排他的|[ **排他** ] ボックスが選択されている場合、データベースは排他モードで開き、一度に1人のユーザーのみがアクセスできます。 排他モードで実行すると、パフォーマンスが向上します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**EXCLUSIVE**キーワードを使用します。|  
|Net スタイル|Paradox データへのアクセス時に使用するネットワークアクセススタイル (Paradox 3 の場合*は "3.x")*。*x* または "4." *x*" は、Paradox 4 を対象としています。*x* または5。*x*。 "3" に設定できます。*x*"または" 4.*x*"バージョンが Paradox 4 の場合。*x* または5。*x*;バージョンが Paradox 3 の場合。*x*の場合、スタイルは "3" にする必要があります。*x*"。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**PARADOXNETSTYLE**キーワードを使用します。|  
|ページタイムアウト|ページ (使用されていない場合) が削除される前にバッファーに残ったままになる時間を秒単位で指定します。 既定値は 600 1/10 (60 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータソースに適用されます。<br /><br /> 固有の遅延が発生したため、ページタイムアウトを0にすることはできません。 ページタイムアウトオプションがその値より下に設定されている場合でも、ページタイムアウトを固有の遅延より小さくすることはできません。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**PAGETIMEOUT**キーワードを使用します。|  
|[読み取り専用]|データベースを読み取り専用として指定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**READONLY**キーワードを使用します。|  
|ディレクトリの選択|アクセスするファイルが格納されているディレクトリを選択できるダイアログボックスを表示します。<br /><br /> データソースディレクトリを定義するときは、最もよく使用されるファイルが置かれているディレクトリを指定します。 ODBC ドライバーでは、このディレクトリが既定のディレクトリとして使用されます。 頻繁に使用する場合は、他のファイルをこのディレクトリにコピーします。 または、次のようにディレクトリ名を指定して、SELECT ステートメント内のファイル名を修飾することもできます。<br /><br /> \*C:\MYDIR\EMP から選択<br /><br /> または、 **SQLSetConnectOption** 関数を SQL_CURRENT_QUALIFIER オプションと共に使用して、新しい既定のディレクトリを指定することもできます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|  
|ネットワークディレクトリの選択|Pdoxusrs.net ファイル (Paradox 4) が含まれているため、Paradox ロックデータベースを含むディレクトリの完全パスです。*x*) または Paradox.net ファイル (Paradox 5)。*x*)。 ディレクトリにこれらのファイルのいずれかが含まれていない場合は、Paradox ドライバーによって作成されます。 これらのファイルの詳細については、「Paradox のドキュメント」を参照してください。<br /><br /> ネットワークディレクトリを選択する前に、[ **ユーザー名** ] テキストボックスに、Paradox のユーザー名を入力する必要があります。 [ **ネットワークディレクトリの選択** ] をクリックして、ネットワークディレクトリを選択します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**PARADOXNETPATH**キーワードを使用します。|  
|[ユーザー名]|Paradox ユーザー名。 これは、ロックが発生したときに、Paradox ファイルの他のユーザーに表示される名前です。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)への呼び出しで**PARADOXUSERNAME**キーワードを使用します。|
