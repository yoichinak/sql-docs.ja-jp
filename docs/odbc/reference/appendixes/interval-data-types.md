---
description: Interval データ型
title: Interval データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b54996c2f2897e47e05088b1985d190acafaad3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429674"
---
# <a name="interval-data-types"></a>Interval データ型
間隔は、2つの日付と時刻の差として定義されます。 間隔は、2つの異なる方法のいずれかで表されます。 1つは、年数と整数の月数で間隔を表す *年月* 間隔です。 もう1つは、日、分、および秒で間隔を表す *日付と時刻* の間隔です。 この2種類の間隔は異なるため、月ごとに異なる日数を設定できるため、混在させることはできません。  
  
 間隔は一連のフィールドで構成されます。 フィールド間には暗黙的な順序があります。 たとえば、年と月の間隔では、年が最初に、その後に月が続きます。 同様に、日付と時刻の間隔では、各フィールドの順序は日、時、分になります。 間隔の種類の最初のフィールドは、" *先頭* のフィールド" または " *昇順* " フィールドと呼ばれます。 最後のフィールドは、 *末尾* のフィールドと呼ばれます。  
  
 すべての間隔で、先頭のフィールドはグレゴリオ暦の規則によって制限されません。 たとえば、1時間ごとの間隔では、通常の場合と同じように、[時間] フィールドは 0 ~ 23 (含む) に制限されません。 先頭フィールドの後の末尾のフィールドは、グレゴリオ暦の通常の制約に従います。 詳細については、この付録の「 [グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)」を参照してください。  
  
 13の interval SQL データ型と13の interval C データ型があります。 各 interval C データ型では、interval データを格納するために、SQL_INTERVAL_STRUCT と同じ構造体を使用します。 (詳細については、次のセクション「 [C Interval 構造体](../../../odbc/reference/appendixes/c-interval-structure.md)」を参照してください)。SQL データ型の詳細については、「 [Sql データ型](../../../odbc/reference/appendixes/sql-data-types.md)」を参照してください。C データ型の詳細については、「 [c データ型](../../../odbc/reference/appendixes/c-data-types.md)」を参照してください。  
  
|型識別子|インスタンス|説明|  
|---------------------|-----------|-----------------|  
|MONTH|年月|2つの日付の間の月数。|  
|YEAR|年月|2つの日付間の年数。|  
|YEAR_TO_MONTH|年月|2つの日付間の年と月の数。|  
|DAY|日時|2つの日付の間の日数。|  
|HOUR|日時|2つの日付/時刻の間の時間数。|  
|MINUTE|日時|2つの日付/時刻の間の分数。|  
|SECOND|日時|2つの日付/時刻の間の秒数。|  
|DAY_TO_HOUR|日時|2つの日付/時刻の間の日数/時間。|  
|DAY_TO_MINUTE|日時|2つの日付/時刻の間の日数/時間/分。|  
|DAY_TO_SECOND|日時|2つの日付/時刻の間の日数/時間/分/秒。|  
|HOUR_TO_MINUTE|日時|2つの日付/時刻の間の時間数/分。|  
|HOUR_TO_SECOND|日時|2つの日付/時刻の間の時間数/分/秒。|  
|MINUTE_TO_SECOND|日時|2つの日付/時刻の間の分数 (秒単位)。|  
  
 このセクションでは、次のトピックを扱います。  
  
-   [C Interval 構造体](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Interval データ型の精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Interval のリテラル](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Interval データ型での既定の先頭有効桁数と秒小数部分のオーバーライド](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
