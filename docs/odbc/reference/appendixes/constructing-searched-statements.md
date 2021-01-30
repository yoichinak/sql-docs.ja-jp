---
description: 検索ステートメントの構築
title: 検索されるステートメントの構築 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7928e3c730a7431d7f94a90a85073a3c818ae31
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99165397"
---
# <a name="constructing-searched-statements"></a>検索ステートメントの構築
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 位置指定の update ステートメントと delete ステートメントをサポートするために、カーソルライブラリは、配置されたステートメントから検索される **update** または **delete** ステートメントを構築します。 データのブロックでの **SQLGetData** の呼び出しをサポートするために、カーソルライブラリは検索された **SELECT** ステートメントを構築して、現在のデータ行を含む結果セットを作成します。 これらの各ステートメントでは、 **where** 句によって、 **sqlcolattribute** の SQL_DESC_SEARCHABLE フィールド識別子に SQL_PRED_SEARCHABLE または SQL_PRED_BASIC を返すバインド列ごとに、キャッシュに格納されている値が列挙されます。  
  
> [!CAUTION]  
>  現在の行を識別するためにカーソルライブラリによって構築された **where** 句は、行の識別、別の行の識別、または複数の行の識別に失敗することがあります。  
  
 位置指定の update または delete ステートメントが複数の行に影響する場合、カーソルライブラリはカーソルが置かれている行の行の状態の配列のみを更新し、SQL_SUCCESS_WITH_INFO と SQLSTATE 01001 (カーソル操作の競合) を返します。 ステートメントで行が識別されない場合、カーソルライブラリでは行の状態の配列が更新されず、SQL_SUCCESS_WITH_INFO と SQLSTATE 01001 (カーソル操作の競合) が返されます。 アプリケーションは **SQLRowCount** を呼び出して、更新または削除された行の数を判断できます。  
  
 **SQLGetData** の呼び出しのためにカーソルを移動するために使用される **SELECT** 句が複数の行を識別する場合、 **SQLGetData** は正しいデータを返すとは限りません。 行が識別されない場合、 **SQLGetData** は SQL_NO_DATA を返します。  
  
 アプリケーションが次のガイドラインに準拠している場合、カーソルライブラリによって構築された **where** 句は、現在の行を一意に識別する必要があります。ただし、データソースに重複する行が含まれている場合など、これが不可能な場合を除きます。  
  
-   **行を一意に識別する列をバインドします。** バインドされた列が行を一意に識別しない場合、カーソルライブラリによって構築される **where** 句によって複数の行が識別されることがあります。 位置指定の update ステートメントまたは delete ステートメントでは、このような句によって複数の行が更新または削除される可能性があります。 **SQLGetData** の呼び出しでは、このような句が原因で、ドライバーが間違った行のデータを返すことがあります。 一意キーのすべての列をバインドすることで、各行が一意に識別されるようになります。  
  
-   **切り捨てが行われない大きさのデータバッファーを割り当てます。** カーソルライブラリのキャッシュは、 **SQLBindCol** を使用して結果セットにバインドされる行セットバッファー内の値のコピーです。 データがこれらのバッファーに配置されるときに切り捨てられる場合は、キャッシュ内でも切り捨てられます。 切り捨てられた値から構築された **where** 句は、データソース内の基になる行を正しく識別できない場合があります。  
  
-   **バイナリ C データに対して null 以外の長さのバッファーを指定します。** **SQLBindCol** の *StrLen_or_IndPtr* 引数が null でない場合にのみ、カーソルライブラリはキャッシュ内に長さバッファーを割り当てます。 *TargetType* 引数が SQL_C_BINARY 場合、カーソルライブラリでは、データから **where** 句を作成するためにバイナリデータの長さが必要になります。 SQL_C_BINARY 列の長さバッファーがなく、アプリケーションが **SQLGetData** を呼び出した場合、または配置された update ステートメントまたは delete ステートメントを実行しようとした場合、カーソルライブラリは SQL_ERROR と SQLSTATE SL014 を返します (位置指定要求が発行され、すべての列カウントフィールドがバッファーに格納されているわけではありません)。  
  
-   **Null 値を許容する列に null 以外の長さのバッファーを指定します。** **SQLBindCol** の *StrLen_or_IndPtr* 引数が null でない場合にのみ、カーソルライブラリはキャッシュ内に長さバッファーを割り当てます。 SQL_NULL_DATA は長さバッファーに格納されるため、カーソルライブラリでは、長さバッファーが指定されていないすべての列が null 非許容であると見なされます。 Null 値を許容する列に長さの列が指定されていない場合、カーソルライブラリは、列のデータ値を使用する **where** 句を構築します。 この句では、行が正しく識別されません。
