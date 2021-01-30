---
description: SQLPostInstallerError 関数
title: Sqlpostインストーラ Error 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72f3059e53e68cce0fc40286ae7c02d0e7eb38bb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204519"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **要約**  
 **Sqlpostインストーラエラー** は、ドライバーまたはトランスレーターセットアップライブラリが、 **configdriver**、 **Configdriver**、および **configdriver** 関数のエラーをインストーラーのエラーキューに報告するためのメカニズムを提供します。 アプリケーションは、この API を使用しません。エラーを取得するには、 **Sqlインストーラエラー** を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引数  
 *fErrorCode*  
 代入インストーラーのエラーコードです。  
  
 *szErrorMsg*  
 代入エラーメッセージのテキスト。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS または SQL_ERROR。  
  
## <a name="diagnostics"></a>診断  
 **Sqlpostインストーラエラー** は、それ自体のエラー値を通知しません。 エラーがインストーラーエラーキューに正常にポストされた場合 ( **Sqlインストーラエラー** を使用して取得可能)、SQL_SUCCESS が返されます。 *Dwerrorcode* 引数の値が、指定されたインストーラーエラーコードのいずれでもない場合、SQL_ERROR が返されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーの追加、変更、または削除|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|データソースの追加、変更、または削除|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|翻訳オプションの設定|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
