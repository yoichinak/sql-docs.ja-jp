---
description: 動作変更および ODBC 3.x ドライバー
title: 動作の変更と ODBC 3.x ドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43f64aa4b627130308ea920918c2de6d98116020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411338"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>動作変更および ODBC 3.x ドライバー
環境属性 SQL_ATTR_ODBC_VERSION は *、odbc 2.x 動作を* 行う必要があるか *、odbc 3.x* 動作を表示する必要があるかどうかをドライバーに示します。 SQL_ATTR_ODBC_VERSION 環境属性がどのように設定されるかは、アプリケーションによって異なります。 ODBC *3.x*アプリケーションは、 **SQLAllocHandle**を呼び出して環境ハンドルを割り当て、 **SQLAllocHandle**を呼び出して接続ハンドルを割り当てる前に、 **SQLSetEnvAttr**を呼び出してこの属性を設定する必要があります。 失敗した場合、ドライバーマネージャーは、 **SQLAllocHandle**への呼び出し時に SQLSTATE HY010 (関数シーケンスエラー) を返します。  
  
> [!NOTE]  
>  動作の変更とアプリケーションの動作のしくみの詳細については、「 [動作の変更](../../../odbc/reference/develop-app/behavioral-changes.md)」を参照してください。  
  
 Odbc *3.x アプリケーションと* *odbc 2.x アプリケーションで*再コンパイルされた odbc 2.X *3.x*アプリケーションは、 **SQLSetEnvAttr**を呼び出しません。 ただし、環境ハンドルを割り当てるために**SQLAllocHandle**ではなく**sqlallocenv**を呼び出します。 このため、アプリケーションがドライバーマネージャーで **Sqlallocenv** を呼び出すと、ドライバーマネージャーはドライバーで **SQLAllocHandle** と **SQLSetEnvAttr** を呼び出します。 したがって、ODBC *3. x* ドライバーは、この属性が設定されている場合、常にカウントできます。  
  
 ODBC_STD compile フラグを使用してコンパイルされた標準準拠のアプリケーションが **Sqlallocenv** を呼び出す場合 ( **SQLALLOCENV** が ISO で非推奨とされているために発生する可能性があります)、呼び出しはコンパイル時に **SQLAllocHandleStd** にマップされます。 実行時に、アプリケーションは **SQLAllocHandleStd**を呼び出します。 ドライバーマネージャーは、SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC3 に設定します。 **SQLAllocHandleStd**の呼び出しは、 *handletype*が SQL_HANDLE_ENV で**SQLAllocHandle**を呼び出す場合と同じです。また、 **SQLSetEnvAttr**を SQL_OV_ODBC3 に設定する場合は、SQL_ATTR_ODBC_VERSION を呼び出します。  
  
 特定のドライバーアーキテクチャでは、接続に応じて、ドライバー*が odbc 2.x ドライバーまた**は odbc 3.x*ドライバーのいずれかとして表示される必要があります。 この場合、ドライバーは実際にはドライバーではなく、ドライバーマネージャーと別のドライバーの間にあるレイヤーです。 たとえば、ODBC Spy のようなドライバーを模倣する場合があります。 別の例では、EDA/SQL のようなゲートウェイとして機能する場合があります。 ODBC 3.x*ドライバーと*して表示されるようにするには、このようなドライバーは**SQLAllocHandle**をエクスポートでき、odbc 2.x ドライバーとして表示される必要があります。では、 **sqlallocconnect**、 *3.x* **sqlallocconnect**、および**sqlallocconnect**をエクスポートできなければなりません。 環境、接続、またはステートメントが割り当てられると、ドライバーマネージャーは、このドライバーが **SQLAllocHandle**をエクスポートするかどうかを確認します。 ドライバーが動作するため、ドライバーマネージャーはドライバーで **SQLAllocHandle** を呼び出します。 ドライバーが ODBC 2.x ドライバーで動作している場合、ドライバーは、必要に応じて、 **SQLAllocHandle**への呼び出しを**sqlallocconnect**、 **sqlallocconnect**、または**sqlallocconnect**にマップする必要が*あります。* また *、ODBC 2.x*ドライバーとして動作する場合は、 **SQLSetEnvAttr**呼び出しで何もする必要はありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Datetime データ型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C データ型の下位互換性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [固定長のブックマーク](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo のサポート](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA を返す](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [データを挿入するための SQLSetPos の呼び出し](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [序数での読み込み](../../../odbc/reference/appendixes/loading-by-ordinal.md)
