---
description: プロジェクトの設定 (型のマッピング) (DB2ToSQL)
title: プロジェクトの設定 (型のマッピング) (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fc7abeb4eec6d25e183db5ffcf1923185016b913
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492545"
---
# <a name="project-settings-type-mapping-db2tosql"></a>プロジェクトの設定 (型のマッピング) (DB2ToSQL)
[ **プロジェクトの設定** ] ダイアログボックスの [型マッピング] ページには、SSMA が DB2 データ型をデータ型に変換する方法をカスタマイズする設定が含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[型マッピング] ページは、[ **プロジェクトの設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   すべての今後の SSMA プロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックし、[移行先の **バージョン** ] ドロップダウンから表示または変更が必要な設定の [移行プロジェクトの種類] を選択して、左側のウィンドウの下部にある [ **型マッピング** ] をクリックします。  
  
-   現在のプロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックし、左側のウィンドウの下部にある [ **型マッピング** ] をクリックします。  
  
現在のオブジェクトまたはオブジェクトのクラスの設定を指定するには、プライマリ SSMA ウィンドウの [ **型マッピング** ] タブを使用します。  
  
## <a name="options"></a>オプション  
次の表は、[ **型マッピング** ] タブのオプションを示しています。  
  
**ソースの種類**  
マップされた DB2 データ型。  
  
**ターゲットの種類**  
指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] た DB2 データ型のターゲットデータ型。  
  
既定の SSMA for DB2 の型マッピングについては、次のセクションの表を参照してください。  
  
**追加**  
[マッピング] ボックスの一覧にデータ型を追加する場合にクリックします。  
  
**[編集]**  
[マッピング] ボックスの一覧で選択したデータ型を編集する場合にクリックします。  
  
**Remove**  
クリックすると、選択したデータ型マッピングが [マッピング] ボックスの一覧から削除されます。  
  
**既定値にリセット**  
クリックすると、[型マッピング] の一覧が SSMA の既定値にリセットされます。  
  
## <a name="default-type-mappings"></a>既定の型マッピング  
SSMA for DB2 では、引数、列、ローカル変数、戻り値に対してカスタムの型マッピングを設定できます。 引数と戻り値の型の既定のマッピングはほぼ同じです。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>既定の引数の型と戻り値の型のマッピング  
次の表に、引数と戻り値の既定のデータ型マッピングを示します。  
  
|DB2 データ型|既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|INT|  
|blob (blob)|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|decimal|float [53]|  
|double precision|float [53]|  
|float|float [53]|  
|INT|INT|  
|整数 (integer)|INT|  
|long|varchar(max)|  
|長生|varbinary(max)|  
|long raw [ \* ..8000]<sup>\*</sup>|varbinary [ \* ]|  
|long raw [8001.. \* ]<sup>\*</sup>|varbinary(max)|  
|national char|nvarchar(max)|  
|各国語文字の変化|nvarchar(max)|  
|national character|nvarchar(max)|  
|各国語文字の変化<sup>\*\*</sup>|nvarchar(max)|  
|各国語文字の変化<sup>\*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|INT|  
|raw|varbinary(max)|  
|real|float [53]|  
|rowid|UNIQUEIDENTIFIER|  
|signtype|smallint|  
|smallint|smallint|  
|string|varchar(max)|  
|timestamp|datetime2|  
|ローカルタイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|タイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>\*</sup> 戻り値の型マッピングにのみ適用されます。  
  
<sup>\*\*</sup> 引数の型マッピングにのみ適用されます。  
  
### <a name="default-column-type-mapping"></a>既定の列の型マッピング  
次の表に、列の既定の型マッピングを示します。  
  
|DB2 データ型|既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob (blob)|varbinary(max)|  
|char|char|  
|char varying [ \* .. \* ]|varchar [ \* ]|  
|char [ \* .. \* ]|char [ \* ]|  
|character|char|  
|文字の変化 [ \* .. \* ]|varchar [ \* ]|  
|文字 [ \* .. \* ]|char [ \* ]|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [ \* .. \* ]|dec [ \* ] [0]|  
|dec [ \* .. \* ][\*..\*]|dec [ \* ] [ \* ]|  
|decimal|10進数 [38] [0]|  
|decimal [ \* .. \* ]|decimal [ \* ] [0]|  
|decimal [ \* .. \* ][\*..\*]|decimal [ \* ] [ \* ]|  
|double precision|float [53]|  
|float|float [53]|  
|float [ \* ..53]|float [ \* ]|  
|float [54.. \* ]|float [53]|  
|INT|INT|  
|整数 (integer)|INT|  
|long|varchar(max)|  
|長生|varbinary(max)|  
|long raw [ \* ..8000]|varbinary [ \* ]|  
|long raw [8001.. \* ]|varbinary(max)|  
|long varchar|varchar(max)|  
|long [ \* ..8000]|varchar [ \* ]|  
|long [8001.. \* ]|varchar(max)|  
|national char|nchar|  
|national char varying [ \* .. \* ]|nvarchar [ \* ]|  
|national char [ \* .. \* ]|nchar [ \* ]|  
|national character|nchar|  
|各国語文字の変化 [ \* .. \* ]|nvarchar [ \* ]|  
|national character [ \* .. \* ]|nchar [ \* ]|  
|nchar|nchar|  
|nchar [ \* ]|nchar [ \* ]|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|数値 [ \* .. \* ]|数値 [ \* ]|  
|数値 [ \* .. \* ][\*..\*]|数値 [ \* ] [ \* ]|  
|numeric|numeric|  
|数値 [ \* .. \* ]|数値 [ \* ]|  
|数値 [ \* .. \* ][\*..\*]|数値 [ \* ] [ \* ]|  
|nvarchar2 [ \* .. \* ]|nvarchar [ \* ]|  
|未加工 [ \* .. \* ]|varbinary [ \* ]|  
|real|float [53]|  
|rowid|UNIQUEIDENTIFIER|  
|smallint|smallint|  
|timestamp|datetime2|  
|ローカルタイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|ローカルタイムゾーンを持つタイムスタンプ [ \* .. \* ]|datetimeoffset [ \* ]|  
|タイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|タイムゾーンを持つタイムスタンプ [ \* .. \* ]|datetimeoffset [ \* ]|  
|タイムスタンプ [ \* .. \* ]|datetime2 [ \* ]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [ \* .. \* ]|UNIQUEIDENTIFIER|  
|varchar [ \* .. \* ]|varchar [ \* ]|  
|varchar2 [ \* .. \* ]|varchar [ \* ]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>既定のローカル変数の型マッピング  
次の表は、ローカル変数の既定の型マッピングを示しています。  
  
|DB2 データ型|既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|INT|  
|BLOB|varbinary(max)|  
|ブール型|bit|  
|Char|char|  
|char varying [ \* ..8000]|varchar [ \* ]|  
|文字の変化 [8001.. \* ]|varchar(max)|  
|char [ \* ..8000]|char [ \* ]|  
|char [8001.. \* ]|varchar(max)|  
|文字|char|  
|文字の変化 ( \* ..8000]|varchar [ \* ]|  
|文字の変化 [8001.. \* ]|varchar(max)|  
|文字 [ \* ..8000]|char [ \* ]|  
|文字 [8001.. \* ]|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [ \* .. \* ]|dec [ \* ] [0]|  
|dec [ \* .. \* ][\*..\*]|dec [ \* ] [ \* ]|  
|decimal|10進数 [38] [0]|  
|decimal [ \* .. \* ]|decimal [ \* ] [0]|  
|decimal [ \* .. \* ][\*..\*]|decimal [ \* ] [ \* ]|  
|double precision|float [53]|  
|Float|float [53]|  
|float [ \* ..53]|float [ \* ]|  
|float [54.. \* ]|float [53]|  
|int|INT|  
|Integer|INT|  
|整数 [ \* .. \* ]|数値 [ \* ] [0]|  
|Long|varchar(max)|  
|長生|varbinary(max)|  
|long raw [ \* ..8000]|varbinary [ \* ]|  
|long raw [8001.. \* ]|varbinary(max)|  
|national char|nchar|  
|national char varying [ \* ..4000]|nvarchar [ \* ]|  
|national char varying [4001.. \* ]|nvarchar(max)|  
|national char [ \* ..4000]|nchar [ \* ]|  
|national char [4001.. \* ]|nvarchar(max)|  
|national character|nchar|  
|national character [ \* ..4000]|nvarchar [ \* ]|  
|national 文字 [4001.. \* ]|nvarchar(max)|  
|各国語文字の変化 [ \* ..4000]|nvarchar [ \* ]|  
|各国語文字のさまざまな [4001.. \* ]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [ \* ..4000]|nchar [ \* ]|  
|nchar [4001.. \* ]|nvarchar(max)|  
|nchar の変化 [ \* ..4000]|nvarchar [ \* ]|  
|nchar の変化 [4001.. \* ]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|数値|float [53]|  
|数値 [ \* .. \* ]|数値 [ \* ]|  
|数値 [ \* .. \* ][\*..\*]|数値 [ \* ] [ \* ]|  
|数値|数値 [38] [0]|  
|数値 [ \* .. \* ]|数値 [ \* ]|  
|数値 [ \* .. \* ][\*..\*]|数値 [ \* ] [ \* ]|  
|nvarchar2 [ \* ..4000]|nvarchar [ \* ]|  
|nvarchar2 [4001.. \* ]|nvarchar(max)|  
|pls_integer|INT|  
|未加工 [ \* ..8000]|varbinary [ \* ]|  
|未加工 [8001.. \* ]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|smallint|  
|Smallint|smallint|  
|文字列 [ \* ..8000]|varchar [ \* ]|  
|文字列 [8001.. \* ]|varchar(max)|  
|timestamp|datetime2|  
|ローカルタイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|タイムゾーンを使用したタイムスタンプ|datetimeoffset|  
|ローカルタイムゾーンを持つタイムスタンプ [ \* .. \* ]|datetimeoffset [ \* ]|  
|タイムゾーンを持つタイムスタンプ [ \* .. \* ]|datetimeoffset [ \* ]|  
|タイムスタンプ [ \* .. \* ]|datetime2 [ \* ]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [ \* .. \* ]|UNIQUEIDENTIFIER|  
|varchar [ \* ..8000]|varchar [ \* ]|  
|varchar [8001.. \* ]|varchar(max)|  
|varchar2 [ \* ..8000]|varchar [ \* ]|  
|varchar2 [8001 \* ]|varch a (max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>関連項目  
[ユーザーインターフェイスリファレンス &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
