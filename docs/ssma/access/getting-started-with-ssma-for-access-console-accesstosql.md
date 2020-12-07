---
description: SSMA for Access コンソールでのはじめに (アクセス可能な Sql)
title: SSMA for Access コンソールでのはじめに (アクセス可能な Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1923323699282e40fcca8afa1a8079edd8163c09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426984"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>SSMA for Access コンソールでのはじめに (アクセス可能な Sql)
このセクションでは、Access コンソールアプリケーションを起動して開始する手順について説明します。 また、ここでは、一般的な SSMA コンソールの出力ウィンドウで使用される規則についても説明します。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソールアプリケーションを起動するには、次の手順に従います。  
  
1.  [ **スタート** ] にアクセスし、[ **すべてのプログラム**] をポイントします。  
  
2.  [ **アクセスの SQL Server Migration Assistant] コマンドプロンプト** ショートカットをクリックします。  
  
    ここには、コンソールアプリケーションの使用を開始するための SSMA コンソールの [使用状況] メニューとが表示され `(/? Help)` ます。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
Windows システムでコンソールが正常に起動したら、次の手順を使用して操作できます。  
  
1.  スクリプトファイルを使用して SSMA コンソールを構成します。 このセクションの詳細については、「 [&#41;&#40;スクリプトファイルの作成 ](../../ssma/access/creating-script-files-accesstosql.md)」を参照してください。  
  
2.  [&#41;&#40;変数値ファイルの作成 ](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [サーバー接続ファイルを作成する &#40;、Sql&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [SSMA コンソールを実行すると ](../../ssma/access/executing-the-ssma-console-accesstosql.md) 、プロジェクトのニーズに基づいて sql&#41;&#40;  
  
追加機能:  
  
1.  [パスワードを指定](managing-passwords-accesstosql.md) し、他のウィンドウコンピューターにエクスポート/インポートする  
  
2.  [レポートを生成](generating-reports-accesstosql.md) して、評価/変換とデータ移行のための詳細な xml 出力レポートを表示します。 更新および同期コマンドについては、詳細なエラーレポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力規則  
SSMA スクリプトコマンドとオプションを実行すると、コンソールプログラムによって結果とメッセージ (情報、エラーなど) がコンソールに表示されるか、必要に応じて xml 出力ファイルにリダイレクトされます。 出力の各種類のメッセージは、一意の色で表されます。 たとえば、ホワイトカラーのテキストメッセージは、スクリプトファイルのコマンドを表します。緑色の色は、ユーザー入力のプロンプトを表します。  
  
![SSMA コンソールの出力](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA コンソールの出力")  
  
次の表に示すコンソール出力の色の解釈:  
  
|Color|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラーが発生した|  
|グレー|日付と時刻のタイムスタンプ、ユーザーへのメッセージ|  
|White|スクリプトファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を要求する|  
|シアン|操作の開始、終了、および結果|  
  
## <a name="see-also"></a>関連項目  
[アクセスのための SQL Server Migration Assistant のインストール](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
