---
description: Query メソッド (RDS)
title: Query メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: rothja
ms.author: jroth
ms.openlocfilehash: d65da0531e9387e94f4d22c734821779c53b9639
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724440"
---
# <a name="query-method-rds"></a>Query メソッド (RDS)
は、有効な SQL クエリ文字列を使用して [レコードセット](../ado-api/recordset-object-ado.md)を返します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *レコードセット*  
 **レコードセット**オブジェクトを表すオブジェクト変数です。  
  
 *DataFactory*  
 [RDSServer DataFactory](./datafactory-object-rdsserver.md)オブジェクトを表すオブジェクト変数です。  
  
 *接続*  
 サーバー接続情報を含む **文字列** 値です。 これは、 [Connect](./connect-property-rds.md) プロパティに似ています。  
  
 *クエリ*  
 SQL クエリを含む **文字列** 。  
  
## <a name="remarks"></a>解説  
 クエリでは、データベースサーバーの SQL 言語を使用する必要があります。 実行されたクエリにエラーがある場合は、結果の状態が返されます。 クエリ **メソッドで** は、 **クエリ** 文字列に対する構文チェックは実行されません。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>参照  
 [DataFactory オブジェクト、Query メソッド、および CreateObject メソッドの例 (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)