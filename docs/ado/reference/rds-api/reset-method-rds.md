---
description: Reset メソッド (RDS)
title: Reset メソッド (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
author: rothja
ms.author: jroth
ms.openlocfilehash: fcebd112b389fe98b69b25852ef0504e88890261
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724261"
---
# <a name="reset-method-rds"></a>Reset メソッド (RDS)
指定された並べ替えとフィルターのプロパティに基づいて、クライアント側の **レコードセット** に対して並べ替えまたはフィルター処理を実行します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
 *value*  
 省略可能。 現在の "フィルター処理された" 行セットをフィルター処理する場合は**True** (**既定値)** です。 **False** は、前のフィルターオプションを削除して、元の行セットに対してフィルター処理を行うことを示します。  
  
## <a name="remarks"></a>解説  
 [Sortcolumn](./sortcolumn-property-rds.md)、 [sortcolumn](./sortdirection-property-rds.md)、 [filtervalue](./filtervalue-property-rds.md)、 [filterfilter、](./filtercriterion-property-rds.md)および[filtervalue](./filtercolumn-property-rds.md)プロパティは、クライアント側キャッシュでの並べ替えとフィルター処理の機能を提供します。 並べ替え機能は、1つの列の値でレコードを並べ替えます。 フィルター機能では、検索条件に基づいてレコードのサブセットが表示されますが、完全な [レコードセット](../ado-api/recordset-object-ado.md) はキャッシュ内に保持されます。 **Reset**メソッドは、条件を実行し、現在の**レコードセット**を更新可能な**レコードセット**に置き換えます。  
  
 送信されていない元のデータに変更があった場合、 **Reset** メソッドは失敗します。 まず、 [SubmitChanges](./submitchanges-method-rds.md) メソッドを使用して、読み取り/書き込み **レコードセット**への変更を保存した後、 **Reset** メソッドを使用してレコードの並べ替えまたはフィルター処理を行います。  
  
 行セットに対して複数のフィルターを実行する場合は、 **Reset**メソッドで省略可能な*ブール型*の引数を使用できます。 以下の例は、その方法を示しています。  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [FilterColumn、Filtercolumn、Filtercolumn、SortColumn、および Sortcolumn プロパティと Reset メソッドの例 (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges メソッド (RDS)](./submitchanges-method-rds.md)