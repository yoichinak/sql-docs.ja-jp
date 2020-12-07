---
description: パラメーターの配列の使用
title: パラメーターの配列の使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a592131165e7dc2370ab1d22a3d9eba5f9609dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424414"
---
# <a name="using-arrays-of-parameters"></a>パラメーターの配列の使用
パラメーターの配列を使用するには、アプリケーションは SQL_ATTR_PARAMSET_SIZE の*属性*引数を使用して**SQLSetStmtAttr**を呼び出し、パラメーターのセット数を指定します。 SQL_ATTR_PARAMS_PROCESSED_PTR の*属性*引数を使用して**SQLSetStmtAttr**を呼び出し、エラーセットを含む、処理されたパラメーターのセットの数をドライバーが返すことができる変数のアドレスを指定します。 このメソッドは、SQL_ATTR_PARAM_STATUS_PTR の*属性*引数を使用して**SQLSetStmtAttr**を呼び出し、パラメーター値の各行の状態情報を返す配列をポイントします。 ドライバーは、ステートメント用に保持されている構造体にこれらのアドレスを格納します。  
  
> [!NOTE]  
>  ODBC 2 の場合。*x*パラメーターに複数の値を指定するために、 **sqlparamoptions** が呼び出されました。 ODBC 3 の場合。*x*では、 **sqlparamoptions** の呼び出しが **SQLSetStmtAttr** の呼び出しに置き換えられ、SQL_ATTR_PARAMSET_SIZE と SQL_ATTR_PARAMS_PROCESSED_ARRAY 属性が設定されています。  
  
 このステートメントを実行する前に、アプリケーションは、バインドされている各配列の各要素の値を設定します。 ステートメントが実行されると、ドライバーは、格納されている情報を使用してパラメーター値を取得し、データソースに送信します。可能であれば、ドライバーはこれらの値を配列として送信する必要があります。 パラメーターの配列の使用は、配列内のすべてのパラメーターを使用して SQL ステートメントを実行し、データソースへの単一の呼び出しを行うことによって実装することをお勧めしますが、この機能は現在、Dbms では広く使用できません。 ただし、ドライバーでは、SQL ステートメントを複数回実行し、それぞれに1つのパラメーターセットを使用することで、ドライバーをシミュレートできます。  
  
 アプリケーションでは、パラメーターの配列を使用する前に、アプリケーションで使用されるドライバーによってサポートされていることを確認する必要があります。 この作業を実行する 2 つの方法があります。  
  
-   パラメーターの配列をサポートするために既知のドライバーのみを使用します。 アプリケーションでは、これらのドライバーの名前をハードコーディングすることも、これらのドライバーのみを使用するようにユーザーに指示することもできます。 カスタムアプリケーションと垂直アプリケーションでは、通常、限られたドライバーのセットを使用します。  
  
-   実行時にパラメーターの配列のサポートを確認します。 SQL_ATTR_PARAMSET_SIZE statement 属性を1より大きい値に設定できる場合、ドライバーはパラメーターの配列をサポートします。 汎用アプリケーションと垂直アプリケーションは、通常、実行時にパラメーターの配列のサポートをチェックします。  
  
 パラメーター化された実行での行数と結果セットの可用性は、SQL_PARAM_ARRAY_ROW_COUNTS オプションと SQL_PARAM_ARRAY_SELECTS オプションを指定して **SQLGetInfo** を呼び出すことによって決定できます。 **INSERT**、 **UPDATE**、および**DELETE**ステートメントの場合、SQL_PARAM_ARRAY_ROW_COUNTS オプションは、個々の行数 (各パラメーターセットに1つ) が SQL_PARC_BATCH 使用可能かどうか、または行カウントが 1 (SQL_PARC_NO_BATCH) にロールアップされるかどうかを示します。 **SELECT**ステートメントの場合、SQL_PARAM_ARRAY_SELECTS オプションは、各パラメーターのセット (SQL_PAS_BATCH) に対して結果セットを使用できるかどうか、または1つの結果セットのみが使用可能である (SQL_PAS_NO_BATCH) かどうかを示します。 ドライバーがパラメーターの配列を使用して結果セット生成ステートメントを実行できない場合、SQL_PARAM_ARRAY_SELECTS は SQL_PAS_NO_SELECT を返します。 これは、パラメーターの配列を他の種類のステートメントと共に使用できるかどうかを指定するデータソース固有のものです。特に、これらのステートメントでパラメーターを使用することは、データソース固有であり、ODBC SQL 文法に従わないためです。  
  
 SQL_ATTR_PARAM_OPERATION_PTR statement 属性が指す配列は、パラメーターの行を無視するために使用できます。 配列の要素が SQL_PARAM_IGNORE に設定されている場合、その要素に対応するパラメーターのセットが **Sqlexecute** または **SQLExecDirect** 呼び出しから除外されます。 SQL_ATTR_PARAM_OPERATION_PTR 属性によって示される配列は、アプリケーションによって割り当てられて格納され、ドライバーによって読み取られます。 フェッチされた行が入力パラメーターとして使用されている場合は、パラメーター操作の配列で row status 配列の値を使用できます。  
  
## <a name="error-processing"></a>エラー処理  
 ステートメントの実行中にエラーが発生した場合、実行関数はエラーを返し、行番号変数をエラーを含む行の番号に設定します。 これは、エラーセットを除くすべての行が実行されるかどうか、またはエラーセットの前 (かつ後ではなく) すべての行が実行されるかどうかによって異なります。 ドライバーは、パラメーターのセットを処理するので、SQL_ATTR_PARAMS_PROCESSED_PTR statement 属性で指定されたバッファーを、現在処理されている行の数に設定します。 エラーセット以外のすべてのセットが実行された場合、ドライバーはすべての行が処理された後に、このバッファーを SQL_ATTR_PARAMSET_SIZE に設定します。  
  
 SQL_ATTR_PARAM_STATUS_PTR statement 属性が設定されている場合、 **Sqlexecute** または **SQLExecDirect** は *パラメーターの状態の配列* を返します。この配列は、パラメーターの各セットの状態を示します。 パラメーターの状態配列は、アプリケーションによって割り当てられ、ドライバーによって入力されます。 この要素は、パラメーターの行に対して SQL ステートメントが正常に実行されたかどうか、またはパラメーターのセットの処理中にエラーが発生したかどうかを示します。 エラーが発生した場合、ドライバーは、パラメーター状態配列内の対応する値を SQL_PARAM_ERROR に設定し、SQL_SUCCESS_WITH_INFO を返します。 アプリケーションでは、状態の配列を確認して、どの行が処理されたかを判断できます。 アプリケーションでは、行番号を使用してエラーを修正し、処理を再開することがあります。  
  
 パラメーターの状態の配列の使用方法は、 **SQLGetInfo**の呼び出しによって返される SQL_PARAM_ARRAY_ROW_COUNTS および SQL_PARAM_ARRAY_SELECTS のオプションによって決まります。 **INSERT**、 **UPDATE**、および**DELETE**ステートメントの場合、SQL_PARAM_ARRAY_ROW_COUNTS に対して SQL_PARC_BATCH が返されても、SQL_PARC_NO_BATCH が返された場合は、状態情報がパラメーターの状態の配列に格納されます。 **SELECT**ステートメントの場合、SQL_PARAM_ARRAY_SELECT に対して SQL_PAS_BATCH が返されても、SQL_PAS_NO_BATCH または SQL_PAS_NO_SELECT が返されていない場合は、パラメーターの状態の配列が格納されます。  
  
## <a name="data-at-execution-parameters"></a>実行時データパラメーター  
 長さ/インジケーター配列内のいずれかの値が SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果である場合、これらの値のデータは通常の方法で **sqlputdata** と共に送信されます。 このプロセスの次の側面は、簡単にはわかりにくいので、特別なコメントがあります。  
  
-   ドライバーが SQL_NEED_DATA を返す場合、行番号の変数のアドレスを、データが必要な行に設定する必要があります。 単一値の場合と同様に、アプリケーションは、ドライバーが1つのパラメーターのセット内でパラメーター値を要求する順序について、想定を行うことはできません。 実行時データパラメーターの実行中にエラーが発生した場合は、SQL_ATTR_PARAMS_PROCESSED_PTR statement 属性によって指定されたバッファーが、エラーが発生した行の番号に設定されています。 SQL_ATTR_PARAM_STATUS_PTR statement 属性で指定された行の状態配列の行の状態が SQL_PARAM_ERROR に設定され、 **Sqlexecute**、 **SQLExecDirect**、 **Sqlparamdata**、または **sqlputdata** への呼び出しによって SQL_ERROR が返されます。 **Sqlexecute**、 **SQLExecDirect**、または**sqlparamdata**が SQL_STILL_EXECUTING を返す場合、このバッファーの内容は未定義です。  
  
-   ドライバーは実行時データパラメーターの**SQLBindParameter**の*parametervalueptr*引数の値を解釈しないため、アプリケーションが配列へのポインターを提供する場合、 **sqlparamdata**はこの配列の要素を抽出してアプリケーションに返しません。 代わりに、アプリケーションが指定したスカラー値が返されます。 つまり、 **Sqlparamdata** によって返される値は、アプリケーションがデータを送信するために必要なパラメーターを指定するのに十分ではありません。アプリケーションでは、現在の行番号も考慮する必要があります。  
  
     パラメーターの配列の一部の要素だけが実行時データパラメーターである場合、アプリケーションは、すべてのパラメーターの要素を含む *Parametervalueptr* 内の配列のアドレスを渡す必要があります。 この配列は、実行時データパラメーターではないパラメーターに対して通常解釈されます。 実行時データパラメーターの場合、 **Sqlparamdata** によってアプリケーションに提供される値は、通常、ドライバーが要求しているデータを識別するために使用されます。これは、常に配列のアドレスです。
