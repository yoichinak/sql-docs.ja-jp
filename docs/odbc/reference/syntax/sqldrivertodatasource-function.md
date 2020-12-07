---
description: SQLDriverToDataSource 関数
title: SQLDriverToDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da885e3be81a7a7de04a58bbb92725317477e80e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461143"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 関数
**SQLDriverToDataSource** は ODBC ドライバーの翻訳をサポートしています。 この関数は、ODBC 対応のアプリケーションでは呼び出されません。アプリケーションは **SQLSetConnectAttr**を通じて変換を要求します。 **SQLSetConnectAttr**で指定された*connectionhandle*に関連付けられているドライバーは、指定された DLL を呼び出して、ドライバーからデータソースへのすべてのデータフローの変換を実行します。 既定の変換 DLL は、ODBC 初期化ファイルで指定できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLDriverToDataSource(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引数  
 *fOption*  
 代入オプションの値。  
  
 *fSqlType*  
 代入ODBC SQL データ型。 この引数は、 *rgbValueIn* をデータソースで許容される形式に変換する方法をドライバーに指示します。 有効な SQL データ型の一覧については、「 [Sql データ型](../../../odbc/reference/appendixes/sql-data-types.md)」を参照してください。  
  
 *rgbValueIn*  
 代入変換する値。  
  
 *cbValueIn*  
 代入 *RgbValueIn*の長さ。  
  
 *rgbValueOut*  
 Output変換の結果。  
  
> [!NOTE]  
>  変換 DLL が null ではない場合、この値は終了しません。  
  
 *cbValueOutMax*  
 代入 *RgbValueOut*の長さ。  
  
 *pcbValueOut*  
 Output *RgbValueOut*で返すことができる合計バイト数 (null 終端バイトを除く)。  
  
 文字またはバイナリデータの場合、これが *Cbvalueoutmax*以上の場合、 *rgbValueOut* 内のデータは *cbvalueoutmax* バイトに切り捨てられます。  
  
 その他のすべてのデータ型では、 *Cbvalueoutmax* の値は無視され、 *rgbValueOut* のサイズは、 *fSqlType*で指定された SQL データ型の既定の C データ型のサイズであると見なされます。  
  
 *Pcbvalueout*引数には null ポインターを指定できます。  
  
 *szErrorMsg*  
 Outputエラーメッセージのストレージへのポインター。 変換に失敗した場合を除き、これは空の文字列です。  
  
 *cbErrorMsgMax*  
 代入 *Szerrormsg*の長さ。  
  
 *pcbErrorMsg*  
 Output *Szerrormsg*で返すことができる合計バイト数 (null 終端バイトを除く) へのポインター。 この値が *Cberrormsg*以上の場合、 *szerrormsg* のデータは *cberrormsgmax* から null 終了文字を引いた値に切り捨てられます。 *Pcberrormsg*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 変換が成功した場合は TRUE、変換に失敗した場合は FALSE。  
  
## <a name="comments"></a>コメント  
 ドライバーは **SQLDriverToDataSource** を呼び出して、ドライバーからデータソースに渡されるすべてのデータ (SQL ステートメント、パラメーターなど) を変換します。 変換 DLL では、データの型と変換 DLL の目的によっては、一部のデータが変換されない場合があります。 たとえば、あるコードページから別のコードページに文字データを変換する DLL は、すべての数値とバイナリデータを無視します。  
  
 *Foption*の値は、SQL_ATTR_TRANSLATE_OPTION 属性を指定して**SQLSetConnectAttr**を呼び出すことによって指定された*vparam*の値に設定されます。 これは、特定の翻訳 DLL に対して特定の意味を持つ32ビット値です。 たとえば、特定の文字セットの変換を指定できます。  
  
 *RgbValueIn*と*rgbValueOut*に同じバッファーが指定されている場合は、バッファー内のデータの変換が適切に実行されます。  
  
 *Cbvaluein*、 *cbvalueoutmax*、 *PCBVALUEOUT*は Sdword 型ですが、 **SQLDriverToDataSource**は必ずしも大きなポインターをサポートしているわけではありません。  
  
 **SQLDriverToDataSource**から FALSE が返された場合、変換中にデータの切り捨てが発生した可能性があります。 *Pcbvalueout* (出力バッファーで返すことができるバイト数) が*Cbvalueoutmax* (出力バッファーの長さ) よりも大きい場合、切り捨てが発生しました。 ドライバーは、切り捨てが許容されるかどうかを判断する必要があります。 切り捨てが行われなかった場合は、別のエラーが原因で **SQLDriverToDataSource** から FALSE が返されました。 どちらの場合も、特定のエラーメッセージが *Szerrormsg*に返されます。  
  
 データの変換の詳細については、「 [Translation dll](../../../odbc/reference/develop-app/translation-dlls.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースから返されたデータの変換|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
