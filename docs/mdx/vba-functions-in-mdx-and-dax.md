---
description: MDX および DAX での VBA 関数
title: MDX および DAX の VBA 関数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dcbf0f0321ddc0c1959c4681c0b1dddf49c1aba
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192292"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX および DAX での VBA 関数


  このドキュメントには、MDX でサポートされている [Visual Basic for Applications 関数](/office/vba/Language/Reference/functions-visual-basic-for-applications) で使用できるすべての VBA 関数の参照が含まれています。また、DAX 言語との機能の等価性がある場合、一覧にはメモが含まれます。  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 関数リファレンス  
  
|関数名|サポートされています|Notes|  
|-------------------|---------------|-----------|  
|Abs|DAX、MDX||  
|Array|サポートされていません||  
|Asc|MDX のみ||  
|AscW|MDX のみ||  
|Atn|MDX のみ||  
|CallByName|サポートされていません||  
|CBool|MDX のみ||  
|CByte|MDX のみ||  
|CCur|MDX のみ||  
|CDate|MDX のみ||  
|CDbl|MDX のみ||  
|CDec|MDX のみ||  
|Choose|MDX のみ||  
|Chr|MDX のみ||  
|CInt|MDX のみ||  
|CLng|MDX のみ||  
|CLngLng|サポートされていません||  
|CLngPtr|サポートされていません||  
|command|サポートされていません||  
|Cos|MDX のみ||  
|CreateObject|サポートされていません||  
|CSng|MDX のみ||  
|CStr|MDX のみ||  
|CurDir|サポートされていません||  
|CVar|MDX のみ||  
|CVErr|サポートされていません||  
|Date|MDX のみ|**警告** DAX は、同じ名前の別の関数を実装しています。指定された引数から日付型の値を生成するために使用される日付 (年、月、日) 関数|  
|DateAdd|MDX のみ|**警告** DAX は、同じ名前の別の関数を実装しています。指定された日付を一定 \<dates> \<interval> の間隔でシフトするために使用される DATEADD (, <number_of_intervals>,) 関数|  
|DateDiff|MDX のみ||  
|DatePart|MDX のみ||  
|DateSerial|MDX のみ||  
|DateValue|DAX、MDX||  
|日間|DAX、MDX||  
|DDB|MDX のみ||  
|Dir|サポートされていません||  
|DoEvents|サポートされていません||  
|Environ|サポートされていません||  
|EOF|サポートされていません||  
|エラー|サポートされていません||  
|Exp|DAX、MDX||  
|FileAttr|サポートされていません||  
|FileDateTime|サポートされていません||  
|FileLen|サポートされていません||  
|Assert|サポートされていません|**警告** MDX では、同じ名前の別の関数が実装されています。FILTER (Set_Expression, Logical_Expression) 関数は、指定された引数の検索条件に基づいて、指定されたセットをフィルター処理した結果セットを返します。<br /><br /> **警告** DAX は、同じ名前の別の関数を実装しています。FILTER ( \<table> , \<filter> ) 関数は、指定された引数から別のテーブルまたは式のサブセットを表すテーブルを返します。|  
|Fix|MDX のみ||  
|Format (Visual Basic for Applications)|DAX、MDX||  
|FormatCurrency|サポートされていません||  
|FormatDateTime|サポートされていません||  
|FormatNumber|サポートされていません||  
|FormatPercent|サポートされていません||  
|FreeFile|サポートされていません||  
|FV|MDX のみ||  
|GetAllSettings|サポートされていません||  
|GetAttr|サポートされていません||  
|GetObject|サポートされていません||  
|GetSetting|サポートされていません||  
|Hex|MDX のみ||  
|時間|DAX、MDX||  
|Iif|MDX のみ|**警告** DAX は、IF (logical_test, value_if_true, value_if_false) 関数という名前の同様の関数を実装します。|  
|IMEStatus|サポートされていません||  
|入力|サポートされていません||  
|InputBox|サポートされていません||  
|InStr|MDX のみ||  
|InStrRev|サポートされていません||  
|int|DAX、MDX||  
|IPmt|MDX のみ||  
|IRR|MDX のみ||  
|IsArray|MDX のみ||  
|IsDateMDX のみ||  
|IsEmpty|MDX のみ||  
|IsError|DAX、MDX||  
|IsMissing|MDX のみ||  
|IsNull|MDX のみ||  
|IsNumeric|MDX のみ||  
|IsObject|サポートされていません||  
|Join|サポートされていません||  
|仮定|サポートされていません||  
|LCase|MDX のみ||  
|Left|DAX、MDX||  
|Len|DAX、MDX||  
|Loc|サポートされていません||  
|LOF|サポートされていません||  
|ログ|MDX のみ|**重要** DAX は、同じ名前の別の関数を実装しています。LOG (number, base) 関数。 指定された引数から指定された底に対する数値の対数を返します。|  
|LTrim|MDX のみ||  
|MacID|サポートされていません||  
|MacScript|サポートされていません||  
|Mid|DAX、MDX||  
|分|DAX、MDX||  
|MIRR|MDX のみ||  
|月|DAX、MDX||  
|MonthName|サポートされていません||  
|MsgBox|サポートされていません||  
|Now|DAX、MDX||  
|NPer|MDX のみ||  
|NPV|MDX のみ||  
|Oct|MDX のみ||  
|Partition|MDX のみ||  
|Pmt|MDX のみ||  
|PPmt|MDX のみ||  
|PV|MDX のみ||  
|QBColor|MDX のみ||  
|料金|MDX のみ||  
|Replace|サポートされていません||  
|RGB|MDX のみ||  
|Right|DAX、MDX||  
|Rnd|MDX のみ||  
|Round|DAX、MDX||  
|RTrim|MDX のみ||  
|Second|DAX、MDX||  
|Seek|サポートされていません||  
|Sgn|DAX、MDX||  
|Shell|サポートされていません||  
|Sin|MDX のみ||  
|SLN|MDX のみ||  
|Space|MDX のみ||  
|Spc|サポートされていません||  
|Split|サポートされていません||  
|R-sqr|MDX のみ||  
|Str|MDX のみ||  
|StrComp|MDX のみ||  
|StrConv|MDX のみ||  
|String|MDX のみ||  
|StrReverse|サポートされていません||  
|スイッチ|MDX のみ||  
|SYD|MDX のみ||  
|タブ|サポートされていません||  
|Tan|MDX のみ||  
|Time|サポートされていません||  
|Timer|MDX のみ||  
|TimeSerial|MDX のみ||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|MDX のみ||  
|UBound|サポートされていません||  
|UCase|MDX のみ||  
|Val|MDX のみ||  
|VarType|サポートされていません||  
|平日|DAX、MDX||  
|WeekdayName|サポートされていません||  
|年|DAX、MDX||  
  
