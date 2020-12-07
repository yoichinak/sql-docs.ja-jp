---
description: SSMA for Sybase コンソールを使用したはじめに (SybaseToSQL)
title: SSMA for Sybase コンソールを使用したはじめに (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 34e0a493140a31099dc4b9ed9f6234743bf0c8c1
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235369"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>SSMA for Sybase コンソールを使用したはじめに (SybaseToSQL)
このセクションでは、SSMA for Sybase コンソールアプリケーションを起動して作業を開始する手順について説明します。 ここでは、一般的な SSMA コンソールの出力ウィンドウで使用される規則についても説明します。  
  
## <a name="launching-the-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソールアプリケーションを起動するには、次の手順に従います。  
  
1.  [スタート] にアクセスし、[すべてのプログラム] をポイントします。  
  
2.  [ **Sybase コマンドプロンプトの SQL Server Migration Assistant** ] ショートカットをクリックします。  
  
    ここには、コンソールアプリケーションの使用を開始するための SSMA コンソールの [使用状況] メニューとが表示され `(/? Help)` ます。  
  
## <a name="using-the-ssma-console"></a>SSMA コンソールの使用  
Windows システムでコンソールが正常に起動されたら、次の手順を使用して操作できます。  
  
1.  スクリプトファイルを使用して SSMA コンソールを構成します。 このセクションの詳細については、「 [SybaseToSQL&#41;&#40;スクリプトファイルの作成 ](../../ssma/sybase/creating-script-files-sybasetosql.md)」を参照してください。  
  
2.  [&#40;SybaseToSQL&#41;の変数値ファイルを作成する ](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [サーバー接続ファイルの作成 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [SSMA コンソールを実行するには、プロジェクトのニーズに基づいて、SybaseToSQL&#41;&#40;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) します。 
  
追加機能:  
  
1.  [パスワードを指定](managing-passwords-sybasetosql.md) し、他のウィンドウコンピューターにエクスポート/インポートします。  
  
2.  [レポートを生成](generating-reports-sybasetosql.md) して、評価/変換およびデータ移行のための詳細な xml 出力レポートを表示します。 更新および同期コマンドの詳細なエラーレポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力規則  
SSMA スクリプトコマンドとオプションを実行すると、コンソールプログラムによって、結果とメッセージ (情報やエラーなど) がコンソールに表示されます。また、必要に応じて、xml 出力ファイルにリダイレクトされます。 出力の各種類のメッセージは、一意の色で表されます。 たとえば、ホワイトカラーのテキストメッセージは、スクリプトファイルのコマンドを表します。緑色の色は、ユーザー入力のプロンプトを表します。  
  
![SSMA コンソールの Sybase 出力の例を示すスクリーンショット。](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
コンソール出力の色の解釈を次の表に示します。  
  
|Color|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラーが発生した|  
|グレー|日付と時刻のタイムスタンプ、ユーザーへのメッセージ|  
|White|スクリプトファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を要求する|  
|シアン|操作の開始、終了、および結果|  
  
## <a name="see-also"></a>関連項目  
[SSMA for SAP ASE のインストール &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
