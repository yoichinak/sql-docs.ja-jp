---
description: SubmitChanges メソッド (RDS)
title: SubmitChanges メソッド (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 69a76648c676af5c6420cffde930ac76c096276d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724176"
---
# <a name="submitchanges-method-rds"></a>SubmitChanges メソッド (RDS)
ローカルにキャッシュされたレコードセットと更新可能な [レコードセット](../ado-api/recordset-object-ado.md) の保留中の変更を、 [接続](./connect-property-rds.md) プロパティまたは [URL](./url-property-rds.md) プロパティで指定されたデータソースに送信します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
 *DataFactory*  
 [RDSServer DataFactory](./datafactory-object-rdsserver.md)オブジェクトを表すオブジェクト変数です。  
  
 *接続*  
 RDS で作成された接続を表す **文字列** 値です **。DataControl** オブジェクトの [Connect](./connect-property-rds.md) プロパティ。  
  
 *レコードセット*  
 **レコードセット**オブジェクトを表すオブジェクト変数です。  
  
## <a name="remarks"></a>解説  
 RDS で**SubmitChanges**メソッドを使用するには、先に[Connect](./connect-property-rds.md)、 [Server](./server-property-rds.md)、および[SQL](./sql-property.md)の各プロパティを設定する必要があり**ます。DataControl**オブジェクト。  
  
 同じ**レコードセット**オブジェクトに対して**SubmitChanges**を呼び出した後に[cancelupdate](./cancelupdate-method-rds.md)メソッドを呼び出すと、変更が既にコミットされているため、 **cancelupdate**呼び出しは失敗します。  
  
 変更されたレコードだけが変更され、すべての変更が成功するか、すべての変更が一緒に失敗します。  
  
 **SubmitChanges**は、既定の**RDSServer**オブジェクトでのみ使用できます。 カスタムビジネスオブジェクトでは、この方法を使用できません。  
  
 **Url**プロパティが設定されている場合、 **SubmitChanges**は url で指定された場所に変更を送信します。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [SubmitChanges メソッドの例 (VBScript)](./submitchanges-method-example-vbscript.md)   
 [アドレス帳のコマンドボタン](../../guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate メソッド (RDS)](./cancelupdate-method-rds.md)   
 [Refresh メソッド (RDS)](./refresh-method-rds.md)