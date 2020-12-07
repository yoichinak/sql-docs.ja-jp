---
description: '付録 B: ODBC の状態遷移テーブル'
title: '付録 B: ODBC 状態遷移テーブル |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b81b43d40d3552959ade377cb7b967eb7331b7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411618"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>付録 B: ODBC の状態遷移テーブル
この付録の表は、ODBC 関数が環境、接続、ステートメント、および記述子の状態の遷移をどのように引き起こしているかを示しています。 環境、接続、ステートメント、または記述子の状態は、通常、対応する種類のハンドル (環境、接続、ステートメント、または記述子) を使用する関数を呼び出すことができる場合に指定されます。 次の図に示すように、環境、接続、ステートメント、および記述子の状態は、ほぼ重複しています。 たとえば、接続状態 C5 と C6 およびステートメントの状態 S1 から S12 の正確な重複は、データソースに依存します。これは、トランザクションが異なるデータソース上で開始され、記述子状態 D1i (暗黙的に割り当てられた記述子) は、記述子が関連付けられているステートメントの状態に依存し、状態 D1e (明示的に割り当てられた記述子 各状態の説明については、この付録の「 [環境遷移](../../../odbc/reference/appendixes/environment-transitions.md)、 [接続遷移](../../../odbc/reference/appendixes/connection-transitions.md)、 [ステートメント遷移](../../../odbc/reference/appendixes/statement-transitions.md)、 [記述子遷移](../../../odbc/reference/appendixes/descriptor-transitions.md)」を参照してください。  
  
 環境と接続の状態は、次のように重複しています。  
  
 ![環境と接続の状態の重複](../../../odbc/reference/appendixes/media/app01.gif "用")  
  
 接続とステートメントの状態は、次のように重複しています。  
  
 ![接続とステートメントの状態の重複](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 ステートメントと記述子の状態は、次のように重複しています。  
  
 ![ステートメントと記述子の状態の重複](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 接続と記述子の状態は、次のように重複しています。  
  
 ![接続と記述子の状態の重複](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 遷移テーブル内の各エントリには、次のいずれかの値を指定できます。  
  
-   **--** -この状態は、関数の実行後も変更されません。  
  
-   **E**  

     **_n_** 、 **C_n_**、 **S_n_**、または **D_n_** -環境、接続、ステートメント、または記述子の状態が、指定された状態に移動します。  
 
-   **(Ih)** -関数に無効なハンドルが渡されました。 ハンドルが null ハンドルであるか、正しくない型の有効なハンドルであった場合 (たとえば、ステートメントハンドルが必要なときに接続ハンドルが渡された場合)、関数は SQL_INVALID_HANDLE を返します。それ以外の場合、動作は未定義で、致命的な場合があります。 このエラーは、指定された状態で関数を呼び出した結果として得られる唯一の結果である場合にのみ表示されます。 このエラーは、状態を変更せず、かっこで示されているように、常にドライバーマネージャーによって検出されます。  
  
-   **NS** -次の状態。 ステートメントの遷移は、ステートメントが非同期状態を経ていない場合と同じです。 たとえば、結果セットを作成するステートメントが状態 S1 から state S11 を取得したとします。これは、 **SQLExecDirect** から SQL_STILL_EXECUTING が返されたためです。 状態 S11 の NS 表記法は、ステートメントの遷移が、結果セットを作成する状態 S1 のステートメントと同じであることを意味します。 **SQLExecDirect**がエラーを返す場合、ステートメントは状態 S1 のままです。成功した場合、ステートメントは状態 S5 に移動します。データが必要な場合、ステートメントは state S8 に移動します。まだ実行中の場合、状態は S11 のままです。  

-   **_Xxxxx_**  または **(*XXXXX*)** -transition テーブルに関連する SQLSTATE。ドライバーマネージャーによって検出された SQLSTATEs は、かっこで囲まれています。 関数は SQL_ERROR および指定された SQLSTATE を返しましたが、状態は変化しません。 たとえば、 **SQLPrepare**の前に**sqlexecute**を呼び出すと、SQLSTATE HY010 (関数シーケンスエラー) が返されます。  

> [!NOTE]  
>  テーブルには、状態を変更しない遷移テーブルとは無関係のエラーは表示されません。 たとえば、 **SQLAllocHandle** が環境の状態 E1 で呼び出され、SQLSTATE HY001 (メモリ割り当てエラー) が返された場合、環境は E1 のままです。これは、 **SQLAllocHandle**の環境遷移の表には示されていません。  
  
 環境、接続、ステートメント、または記述子を複数の状態に移行できる場合、考えられる各状態が表示され、1つまたは複数の脚注によって各遷移が行われる条件が示されます。 次の脚注は、どのテーブルにも表示されます。  
  
|脚注|説明|  
|--------------|-------------|  
|b|の前または後。 カーソルは、結果セットの先頭の前、または結果セットの末尾の後に配置されました。|  
|c|現在の関数。 現在の関数は非同期的に実行されていました。|  
|d|データが必要です。 関数は SQL_NEED_DATA を返しました。|  
|e|エラー。 関数は SQL_ERROR を返しました。|  
|i|行が無効です。 カーソルが結果セットの行に配置され、行が削除されたか、または行の操作でエラーが発生しました。 行の状態の配列が存在する場合は、行の行の状態の配列の値が SQL_ROW_DELETED または SQL_ROW_ERROR になりました。 (行の状態の配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性によって示されます)。|  
|nf|見つかりません。 関数は SQL_NO_DATA を返しました。 これは、検索された update ステートメントまたは delete ステートメントの実行後に、 **SQLExecDirect**、 **sqlexecute**、または **sqlparamdata** によって SQL_NO_DATA が返される場合には適用されません。|  
|np|準備されていません。 ステートメントが準備されていません。|  
|nr|結果がありません。 ステートメントでは、結果セットは作成されません。|  
|o|その他の関数。 別の関数が非同期的に実行されました。|  
|p|準備. ステートメントが準備されました。|  
|r|生じ. ステートメントによって、(空の可能性がある) 結果セットが作成されます。|  
|s|正常終了しました。 関数は SQL_SUCCESS_WITH_INFO または SQL_SUCCESS を返しました。|  
|v|有効な行です。 カーソルが結果セットの行に配置され、行が正常に挿入されたか、正常に更新されたか、または行に対する別の操作が正常に完了しました。 行の状態の配列が存在する場合、行の行の状態の配列の値は、SQL_ROW_ADDED、SQL_ROW_SUCCESS、または SQL_ROW_UPDATED でした。 (行の状態の配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性によって示されます)。|  
|x|実行. 関数は SQL_STILL_EXECUTING を返しました。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 この例では、 *Handletype*が SQL_HANDLE_ENV の場合の**sqlfreehandle**の環境状態遷移テーブルの行は次のようになります。  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|HY010|  
  
 *Handletype*が SQL_HANDLE_ENV に設定された環境の状態 E0 で**sqlfreehandle**が呼び出された場合、ドライバーマネージャーは SQL_INVALID_HANDLE を返します。 *Handletype*が SQL_HANDLE_ENV に設定された状態 e1 で呼び出された場合、関数が成功し、関数が失敗した場合、環境は状態 e1 に移行します。 *Handletype*が SQL_HANDLE_ENV に設定された状態で、e2 で呼び出された場合、ドライバーマネージャーは常に SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返し、環境は e2 の状態のままになります。  
  
 状態遷移テーブルを理解するには、どの項目 (環境、接続、ステートメント、または記述子) が参照しているかを理解する必要があります。 型 X の項目のハンドルを関数が受け入れるとします。この関数の X 状態遷移テーブルでは、型 X の項目のハンドルを使用して関数を呼び出す方法について説明します。これは、その項目に影響します。 たとえば、 **Sqldisconnect** は接続ハンドルを受け入れます。 **Sqldisconnect**の接続状態遷移テーブルでは、 **sqldisconnect**が呼び出された接続の状態にどのように影響するかを説明します。  
  
 関数が Y 型の項目のハンドルを受け入れるとします。 Y は X と等しくありません。この関数の X 状態遷移テーブルでは、型 Y の項目に関連付けられている型 X のハンドルを使用して関数を呼び出す方法について説明します。 Y 型の項目に影響します。たとえば、 **sqldisconnect** のステートメント状態遷移テーブルでは、ステートメントが関連付けられている接続のハンドルを使用して呼び出されたときに、 **sqldisconnect** がステートメントの状態にどのように影響するかを説明します。  
  
 この付録には、次のトピックが含まれています。  
  
-   [環境の遷移](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [接続の遷移](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [記述子の遷移](../../../odbc/reference/appendixes/descriptor-transitions.md)
