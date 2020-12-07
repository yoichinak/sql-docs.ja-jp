---
description: SSMA for Oracle コンソール入門 (OracleToSQL)
title: SSMA for Oracle Console (OracleToSQL) を使用したはじめに |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: a403f515c057349c9717422f99b6de15aede566f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463256"
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>SSMA for Oracle コンソール入門 (OracleToSQL)
このセクションでは、Oracle コンソールアプリケーションを起動して開始する手順について説明します。 また、ここでは、一般的な SSMA コンソールの出力ウィンドウで使用される規則についても説明します。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソールアプリケーションを起動するには、次の手順に従います。  
  
1.  [ **スタート** ] にアクセスし、[ **すべてのプログラム**] をポイントします。  
  
2.  [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle コマンドプロンプトの Migration Assistant** ] ショートカットをクリックします。  
  
    ここには、コンソールアプリケーションの使用を開始するための SSMA コンソールの [使用状況] メニューとが表示され `(/? Help)` ます。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
Windows システムでコンソールが正常に起動したら、次の手順を使用して操作できます。  
  
1.  スクリプトファイルを使用して SSMA コンソールを構成します。 このセクションの詳細については、「 [スクリプトファイル &#40;OracleToSQL&#41;の作成 ](../../ssma/oracle/creating-script-files-oracletosql.md) 」を参照してください。  
  
2.  [OracleToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [OracleToSQL&#41;&#40;のサーバー接続ファイルの作成 ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  プロジェクトのニーズに基づいて[SSMA コンソール &#40;OracleToSQL&#41;を実行する](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
追加機能:  
  
1.  [パスワードを指定](managing-passwords-oracletosql.md) し、他のウィンドウコンピューターにエクスポート/インポートする  
  
2.  [レポートを生成](generating-reports-oracletosql.md) して、評価/変換とデータ移行のための詳細な xml 出力レポートを表示します。 更新および同期コマンドについては、詳細なエラーレポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力規則  
SSMA スクリプトコマンドとオプションを実行すると、コンソールプログラムによって結果とメッセージ (情報、エラーなど) がコンソールに表示されるか、必要に応じて xml 出力ファイルにリダイレクトされます。 出力の各種類のメッセージは、一意の色で表されます。 たとえば、ホワイトカラーのテキストメッセージは、スクリプトファイルのコマンドを表します。緑色の色は、ユーザー入力のプロンプトを表します。  
  
![SSMAConsoleOutput_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMAConsoleOutput_Oracle")  
  
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
[SSMA for Oracle のインストール](installing-ssma-for-oracle-oracletosql.md)  
  
