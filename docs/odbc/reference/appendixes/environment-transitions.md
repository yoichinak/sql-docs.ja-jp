---
description: 環境の遷移
title: 環境の移行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cb4366a044f42440eb70934b9f853947e4f3224
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466232"
---
# <a name="environment-transitions"></a>環境の遷移
ODBC 環境には、次の3つの状態があります。  
  
|州|説明|  
|-----------|-----------------|  
|E0|未割り当ての環境|  
|E1|割り当て済みの環境、未割り当ての接続|  
|E2|割り当て済みの環境、割り当てられた接続|  
  
 次の表は、各 ODBC 関数が環境の状態にどのように影響するかを示しています。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(IH)3|E2 [5]<br />HY0104/6|--[4]|  
|(IH)番|(IH)|--[4]|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV されたときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_DBC されたときの遷移を示しています。  
  
 [3] この行は、 *Handletype* が SQL_HANDLE_STMT または SQL_HANDLE_DESC ときの遷移を示しています。  
  
 [4] 有効なハンドルをポイントする*OutputHandlePtr*で**SQLAllocHandle**を呼び出すと、そのハンドルが上書きされます。 これは、アプリケーションプログラミングエラーの可能性があります。  
  
 [5] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されています。  
  
 [6] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されていません。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources ソースと Sqldatasources  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0103|--[1]<br />HY0103|  
  
 [1] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されています。  
  
 [2] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されていません。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)1|--[3]<br />HY0104/4|--[3]<br />HY0104/4|  
|(IH)3|(IH)|--|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV されたときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_DBC されたときの遷移を示しています。  
  
 [3] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されました。  
  
 [4] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されていません。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)1|E0|HY010|  
|(IH)3|(IH)|--[4]<br />E1 [5]|  
|(IH)番|(IH)|--|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV されたときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_DBC されたときの遷移を示しています。  
  
 [3] この行は、 *Handletype* が SQL_HANDLE_STMT または SQL_HANDLE_DESC ときの遷移を示しています。  
  
 [4] 他の割り当て済み接続ハンドルがありました。  
  
 [5] *ハンドル* で指定された接続ハンドルは、割り当てられた唯一の接続ハンドルでした。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField と SQLGetDiagRec  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)1|--|--|  
|(IH)3|(IH)|--|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV されたときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_DBC、SQL_HANDLE_STMT、または SQL_HANDLE_DESC の場合の遷移を示しています。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0103|--|  
  
 [1] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されています。  
  
 [2] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されていません。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0103|HY011|  
  
 [1] 環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されています。  
  
 [2] *属性* 引数が SQL_ATTR_ODBC_VERSION ませんでした。環境に SQL_ATTR_ODBC_VERSION 環境属性が設定されていません。  
  
## <a name="all-other-odbc-functions"></a>その他すべての ODBC 関数  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> Allocated|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
