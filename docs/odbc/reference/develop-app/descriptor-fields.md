---
description: 記述子フィールド
title: 記述子フィールド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56ca1fa7d558101774d10c8daa530fa32f3f7d21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476734"
---
# <a name="descriptor-fields"></a>記述子フィールド
記述子には、列またはパラメーターを完全に記述する *ヘッダー* フィールドと *レコード* フィールドが含まれています。  
  
 記述子には、次のヘッダーフィールドの1つのコピーが含まれています。 ヘッダーフィールドを変更すると、すべての列またはパラメーターに影響します。  

:::row:::
    :::column:::
        SQL_DESC_ALLOC_TYPE  
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_COUNT  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 記述子に0個以上の記述子レコードが含まれています。 各レコードは、記述子の種類に応じて、列またはパラメーターを記述します。 新しい列またはパラメーターがバインドされると、新しいレコードが記述子に追加されます。 列またはパラメーターがバインド解除されると、レコードは記述子から削除されます。 各レコードには、次のフィールドの1つのコピーが含まれています。  

:::row:::
    :::column:::
        SQL_DESC_AUTO_UNIQUE_VALUE  
        SQL_DESC_BASE_COLUMN_NAME  
        SQL_DESC_BASE_TABLE_NAME  
        SQL_DESC_CASE_SENSITIVE  
        SQL_DESC_CATALOG_NAME  
        SQL_DESC_CONCISE_TYPE  
        SQL_DESC_DATA_PTR  
        SQL_DESC_DATETIME_INTERVAL_CODE  
        SQL_DESC_DATETIME_INTERVAL_PRECISION  
        SQL_DESC_DISPLAY_SIZE  
        SQL_DESC_FIXED_PREC_SCALE  
        SQL_DESC_INDICATOR_PTR  
        SQL_DESC_LABEL  
        SQL_DESC_LENGTH  
        SQL_DESC_LITERAL_PREFIX  
        SQL_DESC_LITERAL_SUFFIX  
    :::column-end:::
    :::column:::
        SQL_DESC_LOCAL_TYPE_NAME  
        SQL_DESC_NAME  
        SQL_DESC_NULLABLE  
        SQL_DESC_OCTET_LENGTH  
        SQL_DESC_OCTET_LENGTH_PTR  
        SQL_DESC_PARAMETER_TYPE  
        SQL_DESC_PRECISION  
        SQL_DESC_SCALE  
        SQL_DESC_SCHEMA_NAME  
        SQL_DESC_SEARCHABLE  
        SQL_DESC_TABLE_NAME  
        SQL_DESC_TYPE  
        SQL_DESC_TYPE_NAME  
        SQL_DESC_UNNAMED  
        SQL_DESC_UNSIGNED  
        SQL_DESC_UPDATABLE  
    :::column-end:::
:::row-end:::

 多くのステートメント属性は、記述子のヘッダーフィールドに対応しています。 **SQLSetStmtAttr**の呼び出しによってこれらの属性を設定し、 **SQLSetDescField**を呼び出すことによって対応する記述子ヘッダーフィールドを設定すると、同じ効果が得られます。 同じことが **SQLGetStmtAttr** と **SQLGetDescField**にも当てはまり、どちらも同じ情報を取得します。 記述子関数の代わりにステートメント関数を呼び出すと、記述子ハンドルを取得する必要がないという利点があります。  
  
 次のヘッダーフィールドは、ステートメント属性を設定することによって設定できます。  

:::row:::
    :::column:::
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 このセクションでは、次のトピックを扱います。  
  
-   [レコード カウント](../../../odbc/reference/develop-app/record-count.md)  
  
-   [バインドされた記述子レコード](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [遅延フィールド](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [整合性チェック](../../../odbc/reference/develop-app/consistency-check.md)
