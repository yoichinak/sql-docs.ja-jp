---
description: カーソルの種類およびコンカレンシーの組み合わせ
title: カーソルの種類と同時実行の組み合わせ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae82825f7b5c6f670e111b859ee02ab4ab875626
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412905"
---
# <a name="cursor-type-and-concurrency-combinations"></a>カーソルの種類およびコンカレンシーの組み合わせ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 カーソルの種類は、ユーザーに提供されるカーソルの機能を制御します。 同時実行オプションは、結果セットの更新可能性とロック動作を制御します。  
  
|カーソルの種類|同時実行 (使用できる値)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup> 「 [キーセットドリブンカーソルの使用に関する制限事項」を](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)参照してください。  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK は、SQL_AUTOCOMMIT 接続オプションが SQL_AUTOCOMMIT_OFF に設定されている場合にのみサポートされます。  
  
## <a name="see-also"></a>参照  
 [接続のオプション](../../odbc/microsoft/connect-options.md)
