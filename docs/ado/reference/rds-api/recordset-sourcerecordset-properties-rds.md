---
description: Recordset、SourceRecordset プロパティ (RDS)
title: Recordset、SourceRecordset Properties (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: rothja
ms.author: jroth
ms.openlocfilehash: cdf8a894341343fee7576daed45c75a46857b909
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724299"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset、SourceRecordset プロパティ (RDS)
カスタムビジネスオブジェクトから返される **レコードセット** オブジェクトを示します。  
  
 **適用対象:** [DATACONTROL オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
 *レコードセット*  
 **レコードセット**オブジェクトを表すオブジェクト変数です。  
  
## <a name="remarks"></a>解説  
 **SourceRecordset**プロパティは、カスタムビジネスオブジェクトから返された[レコードセット](../ado-api/recordset-object-ado.md)に設定できます。  
  
 これらのプロパティを使用すると、アプリケーションはカスタムプロセスを使用してバインドプロセスを処理できます。 レコードセットを直接操作し**て、プロパティ**の設定や**レコードセット**の反復処理などのアクションを実行できるように、**レコード**セットにラップされた行セットを受け取ります。  
  
 **SourceRecordset**プロパティを設定するか、スクリプトコードで実行時に**レコードセット**プロパティを読み取ることができます。  
  
 **SourceRecordset** は、読み取り専用プロパティである **Recordset** プロパティとは対照的に、書き込み専用のプロパティです。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [Recordset および SourceRecordset プロパティの例 (VBScript)](./recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset メソッド (RDS)](./createrecordset-method-rds.md)   
 [Query メソッド (RDS)](./query-method-rds.md)