---
description: SQLRateConnection 関数
title: SQLRateConnection 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc6b217e8d9e06c4ab011d15cfe016dfefc91d76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487123"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 関数
**互換性**  
 導入されたバージョン: ODBC 3.81 標準準拠: ODBC  
  
 **まとめ**  
 **SQLRateConnection** は、ドライバーが接続プール内の既存の接続を再利用できるかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>引数  
 *hRequest*  
 代入新しいアプリケーション接続要求を表すトークンハンドル。  
  
 *hCandidateConnection*  
 代入接続プール内の既存の接続。 接続は opened 状態である必要があります。  
  
 *fRequiredTransactionEnlistment リスト*  
 代入TRUE の場合、新しい接続要求 (*Hrequest*) の既存の接続の*hCandidateConnection*を再利用するには、追加の参加が必要です。  
  
 *% Sid*  
 代入 *Frequiredtransactionenlistment* が TRUE の場合、 *transsid* は、要求が参加する DTC トランザクションを表します。 *Frequiredtransactionenlistment*が*FALSE の場合、使用*されている値は無視されます。  
  
 *前に*  
 Output*Hrequest*の*hCandidateConnection*の再利用評価。 この評価は 0 ~ 100 の範囲内で行われます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 ドライバーマネージャーは、この関数から返された診断情報を処理しません。  
  
## <a name="remarks"></a>解説  
 **SQLRateConnection** は、既存の接続が要求と一致するかどうかを示す 0 ~ 100 のスコアを生成します。  
  
|Score|意味 (SQL_SUCCESS が返される場合)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* を *hrequest*に再利用することはできません。|  
|1から98までの任意の値 (含む)|スコアが高いほど、 *hCandidateConnection* が *hrequest*と一致します。|  
|99|意味のない属性には不一致のみがあります。  ドライバーマネージャーは、評価ループを停止する必要があります。|  
|100|完全一致。  ドライバーマネージャーは、評価ループを停止する必要があります。|  
|100を超えるその他の値|*hCandidateConnection* は dead とマークされており、今後の接続要求でも再利用されることはありません。|  
  
 リターンコードが SQL_SUCCESS (SQL_SUCCESS_WITH_INFO を含む) 以外のものである場合、または評価が100より大きい場合、ドライバーマネージャーは接続を dead としてマークします。 この配信不能接続は、今後の接続要求でも再利用されず、CPTimeout が経過すると最終的にタイムアウトになります。 ドライバーマネージャーは、引き続き、プールから別の接続を検出して評価します。  
  
 ドライバーマネージャーが、100より厳密に小さい (99 を含む) 接続を再利用した場合、ドライバーマネージャーは SQLSetConnectAttr (SQL_ATTR_DBC_INFO_TOKEN) を呼び出して、アプリケーションによって要求された状態に接続をリセットします。 ドライバーは、この関数呼び出しで接続をリセットすることはできません。  
  
 *Frequiredtransactionenlistment*が TRUE の場合、再利用するには追加の参加が必要*です (%* = null) か、または参加解除 ( *hCandidateConnection* *= =* null)。 これは、接続を再利用するコストと、接続を再利用する場合にドライバーが接続の参加/参加解除を行う必要があるかどうかを示します。 *Frequiretransactionenlistment*が*FALSE の場合*、ドライバーは、の値を無効にする必要があります。  
  
 ドライバーマネージャーは、 *Henv* と *hCandidateConnection* の親の henv ハンドルが同じであることを保証します。 ドライバーマネージャーは、 *Hrequest* と *hCandidateConnection* に関連付けられているプール ID が同じであることを保証します。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
