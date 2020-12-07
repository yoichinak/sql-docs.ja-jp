---
description: ドライバー 3.5 をドライバー 3.8 にアップグレードする
title: 3.5 ドライバーを 3.8 Driver にアップグレードする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461334"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>ドライバー 3.5 をドライバー 3.8 にアップグレードする
このトピックでは、ODBC 3.5 ドライバーを ODBC 3.8 ドライバーにアップグレードする際のガイドラインと考慮事項について説明します。  
  
##### <a name="version-numbers"></a>バージョン番号  
 次のガイドラインは、バージョン番号に関連しています。  
  
-   ドライバーは、SQL_ATTR_ODBC_VERSION の SQL_OV_ODBC3_80 をサポートし、SQL_OV_ODBC2、SQL_OV_ODBC3、SQL_OV_ODBC3_80 以外の値に対して SQL_ERROR を返す必要があります。 ドライバーマネージャーの将来のバージョンでは、ドライバーが [SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)から SQL_SUCCESS を返す場合、ドライバーが ODBC 対応レベルをサポートしていると想定します。  
  
-   SQL_DRIVER_ODBC_VER が*InfoType*に渡されると、バージョン3.8 ドライバーは**SQLGetInfo**から03.80 を返す必要があります。 ただし、以前のバージョンの Microsoft Windows に含まれていた古いドライバーマネージャーは、ドライバーをバージョン3.5 のドライバーとして扱い、警告を発行します。  
  
     Windows 7 では、ドライバーマネージャーのバージョンは03.80 です。 Windows 8 では、ドライバーマネージャーのバージョンは、SQLGetInfo SQL_DM_VER (*InfoType* パラメーター) を介して03.81 です。 SQL_ODBC_VER は、Windows 7 と Windows 8 の両方でバージョンを03.80 として報告します。  
  
##### <a name="driver-specific-c-data-types"></a>ドライバー固有の C データ型  
 ドライバーは、バージョン3.8 の ODBC アプリケーションで動作するときに、C データ型をカスタマイズできます。 (詳細については、「 [ODBC での C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください)。ただし、3.8 ドライバーがドライバー固有の C 型を実装する必要はありません。 ただし、ドライバーは引き続き C 型の範囲チェックを実行する必要があります。ドライバーマネージャーは、3.8 のドライバーに対してこれを実行しません。 ドライバーの開発を容易にするために、ドライバー固有の C データ型の値は、次の形式で定義できます。  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>ドライバー固有のデータ型、記述子の型、情報の種類、診断の種類、および属性  
 新しいドライバーを開発するときは、データ型、記述子の型、情報の種類、診断の種類、および属性に対してドライバー固有の範囲を使用する必要があります。 ドライバー固有の範囲とその基本型の値については [、「ドライバー固有のデータ型、記述子の型、情報の種類、診断の種類、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)」を参照してください。  
  
##### <a name="connection-pooling"></a>接続プール  
 接続プールの管理を強化するために、ODBC 3.8 では **SQLSetConnectAttr**の SQL_ATTR_RESET_CONNECTION 接続属性が導入されています。 SQL_RESET_CONNECTION_YES は、この属性の唯一の有効な値です。 SQL_ATTR_RESET_CONNECTION は、ドライバーマネージャーが接続プールに接続を配置する直前に設定されます。これにより、ドライバーは他の接続属性を既定値にリセットできます。  
  
 サーバーとの不要な通信を回避するために、ドライバーは接続がプールから再利用された後、リモートサーバーとの次の通信が行われるまで、接続属性のリセットを遅延させることができます。  
  
 SQL_ATTR_RESET_CONNECTION は、ドライバーマネージャーとドライバー間の通信にのみ使用されることに注意してください。 アプリケーションでこの属性を直接設定することはできません。 すべてのバージョン3.8 ドライバーは、この接続属性を実装する必要があります。  
  
##### <a name="streamed-output-parameters"></a>ストリーム出力パラメーター  
 ODBC バージョン3.8 では、ストリーム出力パラメーターが導入されています。これは、出力パラメーターを取得するためのよりスケーラブルな方法です。 (詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください)。この機能をサポートするには、SQL_GETDATA_EXTENSIONS が**SQLGetInfo**呼び出しの*InfoType*である場合、ドライバーは戻り値に SQL_GD_OUTPUT_PARAMS を設定する必要があります。 ストリーム出力パラメーターを使用した SQL 型のサポートは、ドライバーで実装する必要があります。 ドライバーマネージャーでは、無効な SQL の種類に対してエラーは生成されません。 ストリーム出力パラメーターをサポートする SQL 型は、ドライバーで定義されています。  
  
 アプリケーションが **SQLGetData** を使用して、 **sqlparamdata**によって返されるパラメーターとは異なるパラメーターを取得した場合、ドライバーは SQL_ERROR を返します。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>接続操作の非同期実行 (ポーリングメソッド)  
 ドライバーは、さまざまな接続操作の非同期サポートを有効にすることができます。  
  
 Windows 7 以降では、ODBC はポーリングメソッドをサポートしています (詳細については、「 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください)。 バージョン3.8 の ODBC ドライバーでは、接続ハンドルに非同期操作を実装する必要はありません。 ドライバーが接続ハンドルに対して非同期操作を実装していない場合でも、ドライバーは SQL_ASYNC_DBC_FUNCTIONS *InfoType* を実装し、 **SQL_ASYNC_DBC_NOT_CAPABLE**を返します。  
  
 非同期接続操作が有効になっている場合、接続操作の実行時間は、すべての繰り返し呼び出しの合計時間になります。 合計時間が SQL_ATTR_CONNECTION_TIMEOUT 接続属性によって設定された値を超え、操作が完了していない状態で最後に繰り返し呼び出された場合、ドライバーは SQL_ERROR を返し、SQLState HYT01 の診断レコードをログに記録し、"接続タイムアウトが経過しました" というメッセージを記録します。 操作が終了した場合、タイムアウトはありません。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 関数  
 ODBC 3.8 では、接続とステートメントの両方の操作を取り消すために使用される [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)がサポートされています。 **Sqlcancelhandle**をサポートするドライバーは、関数をエクスポートする必要があります。 アプリケーションがステートメントハンドルで **SQLCancel** または **sqlcancelhandle** を呼び出す場合、実行中の同期または非同期接続関数は、ドライバーによってキャンセルされません。 同様に、アプリケーションが接続ハンドルで **Sqlcancelhandle** を呼び出す場合、実行中の同期または非同期のステートメント関数をドライバーで取り消すことはできません。 また、アプリケーションが接続ハンドルで**Sqlcancelhandle**を呼び出すと、ドライバーは参照操作をキャンセルしないようにする必要があります (**SQLBrowseConnect**は SQL_NEED_DATA を返します)。 このような場合、ドライバーは HY010 "関数シーケンスエラー" を返します。  
  
 **Sqlcancelhandle**と非同期接続の両方の操作を同時にサポートする必要はありません。 ドライバーは非同期接続操作をサポートできますが、 **Sqlcancelhandle**はサポートできません。また、その逆も可能です。  
  
##### <a name="suspended-connections"></a>中断された接続  
 ODBC 3.8 Driver Manager では、接続を中断状態にすることができます。 アプリケーションは **Sqldisconnect** を呼び出して、接続に関連付けられているリソースを解放します。 この場合、ドライバーは接続の状態を確認せずに、可能な限り多くのリソースを解放しようとします。 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。  
  
##### <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール  
 Windows 8 の ODBC を使用すると、ドライバーは接続プールの動作をカスタマイズできます。 詳細については、「 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同期実行 (通知方法)  
 ODBC 3.8 では、Windows 8 以降で使用できる非同期操作の通知方法がサポートされています。 詳細については、「 [非同期実行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供の ODBC ドライバー](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
