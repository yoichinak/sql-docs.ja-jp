---
description: DataTypeEnum
title: DataTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: rothja
ms.author: jroth
ms.openlocfilehash: fd0e2226c0b85b10d7da9f4f14e7068aa25b1d2d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974243"
---
# <a name="datatypeenum"></a>DataTypeEnum
[フィールド](../../../ado/reference/ado-api/field-object.md)、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)、または[プロパティ](../../../ado/reference/ado-api/property-object-ado.md)のデータ型を指定します。 対応する OLE DB 型インジケーターは、次の表の説明列にかっこで囲まれています。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|他のデータ型の配列を示すフラグ値。常に別のデータ型定数と結合されます。 ADOX には適用されません。|  
|**adBigInt**|20|8バイト符号付き整数 (DBTYPE_I8) を示します。|  
|**adBinary**|128|バイナリ値 (DBTYPE_BYTES) を示します。|  
|**adBoolean**|11|**ブール**値 (DBTYPE_BOOL) を示します。|  
|**adBSTR**|8|Null で終わる文字列 (Unicode) (DBTYPE_BSTR) を示します。|  
|**adChapter**|136|子行セット (DBTYPE_HCHAPTER) 内の行を識別する4バイトのチャプター値を示します。|  
|**adChar**|129|文字列値 (DBTYPE_STR) を示します。|  
|**adCurrency**|6|通貨の値 (DBTYPE_CY) を示します。 通貨は、小数点の右側に4桁の固定小数点数です。 1万によってスケーリングされた8バイト符号付き整数に格納されます。|  
|**adDate**|7|日付値 (DBTYPE_DATE) を示します。 日付は、double として格納されます。この部分は、1899年12月30日以降の日数を示し、その小数部は1日の端数です。|  
|**adDBDate**|133|日付値 (yyyymmdd) (DBTYPE_DBDATE) を示します。|  
|**adDBTime**|134|時刻値 (hhmmss) (DBTYPE_DBTIME) を示します。|  
|**adDBTimeStamp**|135|日付/時刻スタンプ (yyyymmddhhmmss に billionths の分数を加えたもの) (DBTYPE_DBTIMESTAMP) を示します。|  
|**adDecimal**|14|有効桁数と小数点以下桁数が固定された正確な数値を示します (DBTYPE_DECIMAL)。|  
|**adDouble**|5|倍精度浮動小数点値 (DBTYPE_R8) を示します。|  
|**adEmpty**|0|値を指定しません (DBTYPE_EMPTY)。|  
|**adError**|10|32ビットエラーコード (DBTYPE_ERROR) を示します。|  
|**adFileTime**|64|1601 (DBTYPE_FILETIME) 以降の100ナノ秒間隔の数を表す64ビットの値を示します。|  
|**adGUID**|72|グローバル一意識別子 (GUID) (DBTYPE_GUID) を示します。|  
|**adIDispatch**|9|COM オブジェクト (DBTYPE_IDISPATCH) の **IDispatch** インターフェイスへのポインターを示します。<br /><br /> **メモ** 現在、このデータ型は ADO ではサポートされていません。 使用状況によって予期しない結果が生じる可能性があります。|  
|**adInteger**|3|4バイト符号付き整数 (DBTYPE_I4) を示します。|  
|**adIUnknown**|13|COM オブジェクト (DBTYPE_IUNKNOWN) の **IUnknown** インターフェイスへのポインターを示します。<br /><br /> **メモ** 現在、このデータ型は ADO ではサポートされていません。 使用状況によって予期しない結果が生じる可能性があります。|  
|**adLongVarBinary**|205|Long バイナリ値を示します。|  
|**adLongVarChar**|201|長い文字列値を示します。|  
|**adLongVarWChar**|203|長い null で終わる Unicode 文字列値を示します。|  
|**adNumeric**|131|有効桁数と小数点以下桁数が固定された正確な数値を示します (DBTYPE_NUMERIC)。|  
|**adPropVariant**|138|オートメーション PROPVARIANT (DBTYPE_PROP_VARIANT) を示します。|  
|**adSingle**|4|単精度浮動小数点値 (DBTYPE_R4) を示します。|  
|**adSmallInt**|2|2バイト符号付き整数 (DBTYPE_I2) を示します。|  
|**adTinyInt**|16|1バイト符号付き整数 (DBTYPE_I1) を示します。|  
|**adUnsignedBigInt**|21|8バイト符号なし整数 (DBTYPE_UI8) を示します。|  
|**adUnsignedInt**|19|4バイト符号なし整数 (DBTYPE_UI4) を示します。|  
|**adUnsignedSmallInt**|18|2バイト符号なし整数 (DBTYPE_UI2) を示します。|  
|**adUnsignedTinyInt**|17|1バイト符号なし整数 (DBTYPE_UI1) を示します。|  
|**adUserDefined**|132|ユーザー定義変数 (DBTYPE_UDT) を示します。|  
|**adVarBinary**|204|バイナリ値を示します。|  
|**adVarChar**|200|文字列値を示します。|  
|**adVariant**|12|オートメーション **バリアント** (DBTYPE_VARIANT) を示します。<br /><br /> **メモ** 現在、このデータ型は ADO ではサポートされていません。 使用状況によって予期しない結果が生じる可能性があります。|  
|**adVarNumeric**|139|数値を示します。|  
|**adVarWChar**|202|Null で終わる Unicode 文字列を示します。|  
|**adWChar**|130|Null で終わる Unicode 文字列 (DBTYPE_WSTR) を示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. チャプター|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. DBDATE|  
|AdoEnums. DBTIME|  
|AdoEnums. DBTIMESTAMP|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. LONGVARBINARY|  
|AdoEnums. LONGVARCHAR|  
|AdoEnums. LONGVARWCHAR|  
|AdoEnums|  
|AdoEnums (データ型)|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. UNSIGNEDBIGINT|  
|AdoEnums. UNSIGNEDINT|  
|AdoEnums。 UNSIGNEDSMALLINT|  
|AdoEnums。 UNSIGNEDTINYINT|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums。 VARNUMERIC|  
|AdoEnums. VARWCHAR|  
|AdoEnums|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
        [CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [CreateRecordset メソッド (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)  
        [Type プロパティ (ADO)](../../../ado/reference/ado-api/type-property-ado.md)  
    :::column-end:::
:::row-end:::
