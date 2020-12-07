---
title: ブレークポイント アクションの指定
description: ブレークポイントにヒットし、特定の他の条件が満たされたときに Transact-SQL デバッガーが実行するカスタム タスクであるヒット アクションを指定する方法について説明します。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint action
- Transact-SQL debugger, breakpoint when hit action
ms.assetid: f97f0097-6f51-40c1-b2e0-294a93ce1e1b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 843963d6c056151842fc5f1edaf786ecc0ced79e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036325"
---
# <a name="specify-a-breakpoint-action"></a>ブレークポイント アクションの指定

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ブレークポイント **ヒット時** アクションは、ブレークポイントに対して [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーが実行するカスタム タスクを指定します。 指定したヒット カウントに達し、指定したブレークポイントの条件が満たされると、ブレークポイントに指定されたアクションがデバッガーによって実行されます。

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
##  <a name="action-considerations"></a><a name="BKMK_ActionConsiderations"></a> アクションに関する注意点

ブレークポイントの既定のアクションでは、ヒット カウントとブレークポイントの条件の両方が満たされたときに、実行が中断されます。 **デバッガーでの** ヒット時 [!INCLUDE[tsql](../../includes/tsql-md.md)] アクションの主な用途は、出力メッセージを指定して、デバッガーの **[出力]** ウィンドウに情報を出力することです。  
  
出力メッセージは、デバッグ対象の **からの情報を格納した式を含むテキスト文字列として、** [メッセージを表示する] [!INCLUDE[tsql](../../includes/tsql-md.md)] オプションで指定します。 式には、次の内容が含まれます。  
  
-   中かっこ ({}) に囲まれた [!INCLUDE[tsql](../../includes/tsql-md.md)] 式。 式には、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 変数、パラメーター、および組み込み関数を含めることができます。 例としては、{@MyVariable}、{@NameParameter}、{@@SPID}、{SERVERPROPERTY('ProcessID')} などがあります。  
  
-   次のキーワードのいずれかになります。  
  
    1.  $ADDRESS は、ブレークポイントが設定されているストアド プロシージャまたはユーザー定義関数の名前を返します。 ブレークポイントがエディター ウィンドウに設定されている場合、$ADDRESS は編集されているスクリプト ファイルの名前を返します。 $ADDRESS および $FUNCTION は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーで同じ情報を返します。  
  
    2.  $CALLER は、ストアド プロシージャまたは関数を呼び出した [!INCLUDE[tsql](../../includes/tsql-md.md)] コードの単位の名前を返します。 ブレークポイントがエディター ウィンドウにある場合は、$CALLER は \<No caller available> を返します。 ブレークポイントが、エディター ウィンドウ内のコードから呼び出されるストアド プロシージャまたはユーザー定義関数にある場合は、$CALLER は編集されているファイルの名前を返します。 ブレークポイントが、他のストアド プロシージャまたは関数から呼び出されるストアド プロシージャまたはユーザー定義関数にある場合は、$CALLER は呼び出しているプロシージャまたは関数の名前を返します。  
  
    3.  $CALLSTACK は、現在のストアド プロシージャまたはユーザー定義関数を呼び出したチェーン内の関数の呼び出し履歴を返します。 ブレークポイントがエディター ウィンドウにある場合、$CALLSTACK は編集されているスクリプト ファイルの名前を返します。  
  
    4.  $FUNCTION は、ブレークポイントが設定されているストアド プロシージャまたはユーザー定義関数の名前を返します。 ブレークポイントがエディター ウィンドウに設定されている場合、$FUNCTION は編集されているスクリプト ファイルの名前を返します。  
  
    5.  $PID および $PNAME は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] が実行されているデータベース エンジンのインスタンスを実行しているオペレーティング システム プロセスの ID および名前を返します。 $PID は、SERVERPROPERTY('ProcessID') と同じ ID を返しますが、SERVERPROPERTY('ProcessID') が 10 進値であるのに対して $PID は 16 進数の値である点が異なります。  
  
    6.  $TID および $TNAME は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチを実行しているオペレーティング システム スレッドの ID および名前を返します。 スレッドは、データベース エンジンのインスタンスを実行しているプロセスに関連付けられています。 $TID は SELECT kpid FROM sys.sysprocesses WHERE spid = @@SPID と同じ値を返しますが、kpid が 10 進値であるのに対して $TID は 16 進数の値である点が異なります。  
  
-   "\\{"、" \\}"、" \\" のようにバックスラッシュ記号 ( \\\\) をエスケープ文字とすることで、メッセージ内で中かっことバックスラッシュを使用することもできます。  
  
#### <a name="to-specify-a-when-hit-action"></a>ヒット時アクションを指定するには  
  
1.  エディター ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[ヒット時]** をクリックします。  
  
     または  
  
     **[ブレークポイント]** ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[ヒット時]** をクリックします。  
  
2.  **[ブレークポイントのヒット時]** ダイアログ ボックスで、目的の動作を選択します。  
  
    1.  ブレークポイントにヒットしたときにデバッガーの出力ウィンドウにメッセージを出力するには、 **[メッセージを表示する]** を選択します。  
  
    2.  **[マクロを実行する]** オプションは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは使用できないため、グレーで表示されます。  
  
    3.  ブレークポイントの実行を中断したくない場合は、 **[続けて実行する]** を選択します。 このオプションは、 **[メッセージを表示する]** オプションを選択した場合にのみ有効です。  
  
3.  **[OK]** をクリックして変更を適用するか、 **[キャンセル]** をクリックして変更を適用せずに終了します。  
  
## <a name="see-also"></a>参照  
 [ブレークポイント条件の指定](./specify-a-breakpoint-condition.md)   
 [ヒット カウントの指定](./specify-a-hit-count.md)