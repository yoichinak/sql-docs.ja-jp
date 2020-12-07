---
description: ConfigTranslator 関数
title: ConfigTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b99628b801199c7e2d7fd033e1b0728f1538932
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461274"
---
# <a name="configtranslator-function"></a>ConfigTranslator 関数
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **まとめ**  
 **Configtranslator** は、翻訳者の既定の翻訳オプションを返します。 トランスレーター DLL または別のセットアップ DLL に配置できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 代入親ウィンドウハンドル。 ハンドルが null の場合、この関数はダイアログボックスを表示しません。  
  
 *pvOption*  
 Output32ビット変換オプション。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Configtranslator**から FALSE が返された場合、関連する* \* Pferrorcode*値は、 **sqlpostインストーラエラー**の呼び出しによってインストーラーエラーバッファーにポストされ、 **sqlインストーラエラー**を呼び出すことによって取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*HwndParent*引数が無効であるか、NULL でした。|  
|ODBC_ERROR_DRIVER_SPECIFIC|ドライバーまたはトランスレーター固有のエラー|ODBC インストーラーエラーが定義されていないドライバー固有のエラー。 **Sqlpostインストーラ error**関数の呼び出しの*szerror*引数には、ドライバー固有のエラーメッセージが含まれている必要があります。|  
|ODBC_ERROR_INVALID_OPTION|無効な変換オプション|*Pvoption*引数に無効な値が含まれています。|  
  
## <a name="comments"></a>コメント  
 変換ツールで1つの翻訳オプションのみがサポートされている場合、 **Configtranslator** は TRUE を返し、 *pvoption* を32ビットオプションに設定します。 それ以外の場合は、使用する既定の翻訳オプションを決定します。 **Configtranslator** では、ユーザーが既定の翻訳オプションを選択するダイアログボックスを表示できます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|翻訳オプションを取得する|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|トランスレーターの選択|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|翻訳オプションの設定|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
