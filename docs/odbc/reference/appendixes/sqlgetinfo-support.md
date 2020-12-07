---
description: SQLGetInfo のサポート
title: SQLGetInfo サポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cff18a23c7d8c4526fc86904d75375ed5aaaf5a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471233"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo のサポート
ODBC 2 の場合。*x*アプリケーションが ODBC*3.x ドライバーに*対して**SQLGetInfo**を呼び出すと、次の表の*InfoType*引数がサポートされている必要があります。  
  
|*InfoType*|戻り値|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **メモ:**  この情報の種類は非推奨です。右側の列のビットマスクは非推奨とされます。|データソースでサポートされている **ALTER TABLE** ステートメント内の句を列挙する SQLINTEGER ビットマスク。<br /><br /> サポートされている句を判別するには、次のビットマスクを使用します。<br /><br /> SQL_AT_DROP_COLUMN = 列を削除する機能はサポートされています。 この結果が cascade または restrict になるかどうかは、ドライバーによって定義されます。 (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 1 つの ALTER TABLE ステートメントで複数の列を追加する機能はサポートされています。 このビットは、他の SQL_AT_ADD_COLUMN_XXX ビットまたは SQL_AT_CONSTRAINT_XXX ビットと組み合わせることはできません。 (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> この情報の種類は ODBC 1.0 で導入されました。各ビットマスクには、それが導入されたバージョンのラベルが付けられています。|サポートされているフェッチ方向オプションを列挙する SQLINTEGER ビットマスク。<br /><br /> 次のビットマスクは、どのオプションがサポートされているかを判断するためにフラグと組み合わせて使用されます。<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|**SQLSetPos**の*fLock*引数に対してサポートされているロックの種類を列挙する SQLINTEGER ビットマスク。<br /><br /> サポートされているロックの種類を判断するには、次のビットマスクをフラグと組み合わせて使用します。<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|ODBC 準拠のレベルを示す SQLSMALLINT 値。<br /><br /> SQL_OAC_NONE = なし<br /><br /> SQL_OAC_LEVEL1 = レベル1がサポートされています<br /><br /> SQL_OAC_LEVEL2 = レベル2がサポートされています|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|ドライバーでサポートされている SQL 文法を示す SQLSMALLINT 値。 SQL 準拠レベルの定義については、「 [付録 C: Sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) 」を参照してください。<br /><br /> SQL_OSC_MINIMUM = サポートされている最低限の文法<br /><br /> SQL_OSC_CORE = サポートされているコア文法<br /><br /> SQL_OSC_EXTENDED = サポートされている拡張文法|  
|SQL_POS_OPERATIONS (ODBC 2.0)|**SQLSetPos**でサポートされている操作を列挙する SQLINTEGER ビットマスク。<br /><br /> 次のビットマスクは、どのオプションがサポートされているかを判断するためにフラグと組み合わせて使用されます。<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|サポートされている位置指定 SQL ステートメントを列挙する SQLINTEGER ビットマスク。<br /><br /> サポートされているステートメントを判別するには、次のビットマスクを使用します。<br /><br /> SQL_PS_POSITIONED_DELETE、SQL_PS_POSITIONED_UPDATE、SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|カーソルに対してサポートされている同時実行制御オプションを列挙する SQLINTEGER ビットマスク。<br /><br /> サポートされているオプションを判別するには、次のビットマスクを使用します。<br /><br /> SQL_SCCO_READ_ONLY = カーソルは読み取り専用です。 更新は許可されていません。<br /><br /> SQL_SCCO_LOCK = カーソルは、行を更新できるように、十分なロックレベルを使用します。<br /><br /> SQL_SCCO_OPT_ROWVER = カーソルは、オプティミスティック同時実行制御を使用して、SQLBase ROWID や Sybase TIMESTAMP などの行バージョンを比較します。<br /><br /> SQL_SCCO_OPT_VALUES = カーソルはオプティミスティック同時実行制御を使用して、値を比較します。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|アプリケーションによって行われた変更が、 **SQLSetPos** または位置指定の update または delete ステートメントを使用して、そのアプリケーションによって検出されるかどうかを列挙する SQLINTEGER ビットマスク。<br /><br /> SQL_SS_ADDITIONS = 追加された行はカーソルから参照できます。カーソルは次の行にスクロールできます。 これらの行がカーソルに追加される場所は、ドライバーに依存します。<br /><br /> SQL_SS_DELETIONS = 削除された行はカーソルで使用できなくなり、結果セットに "パンチ穴" を残しません。カーソルが削除された行からスクロールすると、その行に戻ることはできません。<br /><br /> SQL_SS_UPDATES = 行の更新はカーソルに表示されます。カーソルがからスクロールして更新された行に戻ると、カーソルによって返されるデータは、元のデータではなく更新されたデータになります。 このオプションは、キーを更新しない静的カーソルまたはキーセットドリブンカーソルの更新にのみ適用されます。 このオプションは、動的カーソルの場合、または混合カーソルでキーが変更された場合には適用されません。<br /><br /> 同じアプリケーション内の他のユーザーによって結果セットに加えられた変更をアプリケーションが検出できるかどうかは、カーソルの種類によって異なります。|  
  
 Odbc*3.x アプリケーションで*odbc*3.x ドライバーを*使用する場合は、前の表で説明されている*InfoType*引数を使用して**SQLGetInfo**を呼び出すことはできませんが、次の段落に示す ODBC 3 *. x* *InfoType*引数を使用する必要があります。 ODBC 2 で使用される *InfoType* 引数の間には1対1の対応はありません。*x* と ODBC 3 *. x*で使用されているものです。 Odbc 3 *. x* アプリケーションで odbc 2 を操作します。一方、 *x* ドライバーでは、前に説明した *InfoType* 引数を使用する必要があります。  
  
 カーソル属性情報の種類を優先するために、前の表に示した情報の種類の一部は非推奨とされます。 これらの非推奨の情報の種類は、SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY、および SQL_STATIC_SENSITIVITY です。 新しい cursor 属性の型は SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2 です。ここで、XXX は DYNAMIC、FORWARD_ONLY、KEYSET_DRIVEN、または STATIC と等しくなります。 新しい各型は、1つのカーソルの種類のドライバー機能を示しています。 これらのオプションの詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明」を参照してください。
