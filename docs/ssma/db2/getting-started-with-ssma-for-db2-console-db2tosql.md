---
description: SSMA for DB2 Console (DB2ToSQL) を使用したはじめに
title: SSMA for DB2 Console (DB2ToSQL) でのはじめに |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 57cf454c5d13bf4a40325024e51bd19c4d56c446
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985125"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>SSMA for DB2 Console (DB2ToSQL) を使用したはじめに
このセクションでは、DB2 コンソールアプリケーションを起動して開始する手順について説明します。 また、ここでは、一般的な SSMA コンソールの出力ウィンドウで使用される規則についても説明します。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソールアプリケーションを起動するには、次の手順に従います。  
  
1.  [ **スタート** ] にアクセスし、[ **すべてのプログラム**] をポイントします。  
  
2.  [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MIGRATION ASSISTANT For DB2 コマンドプロンプト**] ショートカットをクリックします。  
  
    ここには、コンソールアプリケーションの使用を開始するための SSMA コンソールの [使用状況] メニューとが表示され `(/? Help)` ます。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
Windows システムでコンソールが正常に起動したら、次の手順を使用して操作できます。  
  
1.  スクリプトファイルを使用して SSMA コンソールを構成します。 このセクションの詳細については、「 [スクリプトファイル &#40;DB2ToSQL&#41;の作成 ](../../ssma/db2/creating-script-files-db2tosql.md) 」を参照してください。  
  
2.  [DB2ToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [DB2ToSQL&#41;&#40;のサーバー接続ファイルの作成 ](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  プロジェクトのニーズに基づいて[SSMA コンソール &#40;DB2ToSQL&#41;を実行する](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
追加機能:  
  
1.  [パスワードを管理](./managing-passwords-db2tosql.md) し、他のウィンドウコンピューターにエクスポート/インポートする  
  
2.  [レポートを生成](./generating-reports-db2tosql.md) して、評価/変換とデータ移行のための詳細な xml 出力レポートを表示します。 更新および同期コマンドについては、詳細なエラーレポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力規則  
SSMA スクリプトコマンドとオプションを実行すると、コンソールプログラムによって結果とメッセージ (情報、エラーなど) がコンソールに表示されるか、必要に応じて xml 出力ファイルにリダイレクトされます。 出力の各種類のメッセージは、一意の色で表されます。 たとえば、ホワイトカラーのテキストメッセージは、スクリプトファイルのコマンドを表します。緑色の色は、ユーザー入力のプロンプトを表します。  
  
![SSMAConsoleOutput_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMAConsoleOutput_Oracle")  
  
次の表に示すコンソール出力の色の解釈:  
  
|Color|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラーが発生した|  
|グレー|日付と時刻のタイムスタンプ、ユーザーへのメッセージ|  
|白|スクリプトファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を要求する|  
|シアン|操作の開始、終了、および結果|  
  
## <a name="see-also"></a>参照  
[SSMA for DB2 のインストール](./installing-ssma-for-db2-db2tosql.md)  
