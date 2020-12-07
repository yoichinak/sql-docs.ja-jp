---
description: SSMA for MySQL コンソール入門 (MySQLToSQL)
title: SSMA for MySQL コンソールでのはじめに (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 59df65daf56708a2b30b1e0a75e554750e95cb47
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235189"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>SSMA for MySQL コンソール入門 (MySQLToSQL)
このセクションでは、MySQL コンソールアプリケーションを起動して開始する手順について説明します。 また、ここでは、一般的な SSMA コンソールの出力ウィンドウで使用される規則についても説明します。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソールアプリケーションを起動するには、次の手順に従います。  
  
1.  [ **スタート** ] にアクセスし、[ **すべてのプログラム** ] をポイントします。  
  
2.  [ **SQL Server Migration Assistant For MySQL コマンドプロンプト** ] ショートカットをクリックします。  
  
    ここには、コンソールアプリケーションの使用を開始するための SSMA コンソールの [使用状況] メニューとが表示され `(/? Help)` ます。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
Windows システムでコンソールが正常に起動したら、次の手順を使用して操作できます。  
  
1.  スクリプトファイルを使用して SSMA コンソールを構成します。 このセクションの詳細については、「 [スクリプトファイル &#40;MySQLToSQL&#41;の作成 ](../../ssma/mysql/creating-script-files-mysqltosql.md) 」を参照してください。  
  
2.  [MySQLToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [MySQLToSQL&#41;&#40;のサーバー接続ファイルの作成 ](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  プロジェクトのニーズに基づいて[SSMA コンソール &#40;MySQLToSQL&#41;を実行する](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
追加機能:  
  
1.  [パスワードをセキュリティで保護](managing-passwords-mysqltosql.md) し、他のウィンドウコンピューターにエクスポート/インポートする  
  
2.  [レポートを生成](generating-reports-mysqltosql.md) して、評価/変換とデータ移行のための詳細な xml 出力レポートを表示します。 更新および同期コマンドについては、詳細なエラーレポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力規則  
SSMA スクリプトコマンドとオプションを実行すると、コンソールプログラムによって結果とメッセージ (情報、エラーなど) がコンソールに表示されるか、必要に応じて xml 出力ファイルにリダイレクトされます。 出力の各種類のメッセージは、一意の色で表されます。 たとえば、ホワイトカラーのテキストメッセージは、スクリプトファイルのコマンドを表します。緑色の色は、ユーザー入力のプロンプトを表します。  
  
![SSMA コンソールの MySQL 出力の例を示すスクリーンショット。](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
次の表に示すコンソール出力の色の解釈:  
  
|Color|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラーが発生した|  
|グレー|日付と時刻のタイムスタンプ、ユーザーへのメッセージ|  
|White|スクリプトファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を要求する|  
|シアン|操作の開始、終了、および結果|  
  
## <a name="see-also"></a>参照  
[SSMA for MySQL のインストール](installing-ssma-for-mysql-mysqltosql.md)  
  
