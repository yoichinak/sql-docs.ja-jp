---
description: SQL プロパティ
title: SQL プロパティ |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: rothja
ms.author: jroth
ms.openlocfilehash: 325f739e55bcb2b7d3e7440e9906fad341c01078
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724198"
---
# <a name="sql-property"></a>SQL プロパティ
[レコードセット](../ado-api/recordset-object-ado.md)を取得するために使用するクエリ文字列を示します。  
  
 RDS では、デザイン時に **SQL** プロパティを設定でき [ます。DataControl](./datacontrol-object-rds.md) オブジェクトのオブジェクトタグ、またはスクリプトコードの実行時。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>パラメーター  
 *クエリ*  
 有効な SQL データ要求を含む **文字列** 値です。  
  
 *DataControl*  
 RDS を表すオブジェクト変数です **。DataControl** オブジェクト。  
  
## <a name="remarks"></a>解説  
 一般に、これは (データベースサーバーの言語を使用した) SQL ステートメントです `"Select * from NewTitles"` 。 レコードが正確に一致して更新されるように、更新可能なクエリには、長いバイナリフィールドまたは計算フィールド以外のフィールドを含める必要があります。  
  
 カスタムのサーバー側ビジネスオブジェクトがクライアントのデータを取得する場合、 **SQL** プロパティは省略可能です。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [SQL プロパティの例 (VBScript)](./sql-property-example-vbscript.md)   
 [Connect プロパティ (RDS)](./connect-property-rds.md)   
 [Query メソッド (RDS)](./query-method-rds.md)   
 [Refresh メソッド (RDS)](./refresh-method-rds.md)   
 [SubmitChanges メソッド (RDS)](./submitchanges-method-rds.md)