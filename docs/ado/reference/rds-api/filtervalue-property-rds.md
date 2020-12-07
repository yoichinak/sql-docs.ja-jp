---
description: FilterValue プロパティ (RDS)
title: FilterValue プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f2731f86983f6e2c61f5626970e4fbbb3f09590
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720673"
---
# <a name="filtervalue-property-rds"></a>FilterValue プロパティ (RDS)
レコードのフィルター処理に使用する値を示します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
 *String*  
 レコードをフィルター処理するために使用するデータ値を表す **文字列** 値 ( `'Programmer'` やなど `125` )。  
  
## <a name="remarks"></a>解説  
 [Sortcolumn](./sortcolumn-property-rds.md)、 [sortcolumn](./sortdirection-property-rds.md)、 **filtervalue**、 [filterfilter、](./filtercriterion-property-rds.md)および[filtervalue](./filtercolumn-property-rds.md)プロパティは、クライアント側キャッシュでの並べ替えとフィルター処理の機能を提供します。 並べ替え機能は、1つの列の値でレコードを並べ替えます。 フィルター機能では、検索条件に基づいてレコードのサブセットが表示されますが、完全な [レコードセット](../ado-api/recordset-object-ado.md) はキャッシュに保持されます。 [Reset](./reset-method-rds.md)メソッドは、条件を実行し、現在の**レコードセット**を更新可能な**レコードセット**に置き換えます。  
  
 Null 値を指定すると、型の不一致エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [FilterColumn、Filtercolumn、Filtercolumn、SortColumn、および Sortcolumn プロパティと Reset メソッドの例 (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn プロパティ (RDS)](./filtercolumn-property-rds.md)   
 [Filterfilterproperty (RDS)](./filtercriterion-property-rds.md)   
 [SortColumn プロパティ (RDS)](./sortcolumn-property-rds.md)   
 [SortDirection プロパティ (RDS)](./sortdirection-property-rds.md)