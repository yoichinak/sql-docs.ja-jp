---
description: SQLGetInstalledDrivers 関数
title: Sqlgetdrivers 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0599cb187dee9d3b860f619538b1e0dc148ad58d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421266"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 関数
**互換性**  
 導入されたバージョン: ODBC 1.0  
  
 **まとめ**  
 **Sqlgetinstalled ドライバー** は、システム情報の [ODBC ドライバー] セクションを読み取り、インストールされているドライバーの説明の一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引数  
 *lpszBuf*  
 Outputインストールされているドライバーの説明の一覧。 リスト構造の詳細については、「コメント」を参照してください。  
  
 *cbBufMax*  
 代入 *Lpszbuf*の長さ。  
  
 *pcbBufOut*  
 Output *Lpszbuf*で返された合計バイト数 (null 終端バイトを除く)。 返すことのできるバイト数が *cbBufMax*以上の場合、 *lpszbuf* 内のドライバーの説明の一覧は、 *cbBufMax* から null 終了文字を引いた値に切り捨てられます。 *PcbBufOut*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetのドライバー**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszbuf*引数が NULL または無効であったか、 *cbBufMax*引数が0以下でした。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーで、レジストリの [ODBC ドライバー] セクションが見つかりませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 各ドライバーの説明は null バイトで終了し、リスト全体は null バイトで終了します。 (つまり、2つの null バイトはリストの末尾をマークします)。割り当てられたバッファーがリスト全体を保持するのに十分な大きさでない場合は、エラーなしで一覧が切り捨てられます。 Null ポインターが *Lpszbuf*として渡されると、エラーが返されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーの説明と属性を返す|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
