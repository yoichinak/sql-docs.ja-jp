---
description: Refresh メソッド (RDS)
title: Refresh メソッド (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e6fb32744d64f99beac6c414f1b82581b9fadcb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724274"
---
# <a name="refresh-method-rds"></a>Refresh メソッド (RDS)
[接続](./connect-property-rds.md)プロパティで指定されたデータソースを再クエリし、クエリ結果を更新します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
## <a name="remarks"></a>解説  
 **Refresh**メソッドを使用する前に、 [Connect](./connect-property-rds.md)、 [Server](./server-property-rds.md)、および[SQL](./sql-property.md)の各プロパティを設定する必要があります。 RDS に関連付けられているフォーム上のすべてのデータバインドコントロール。 **DataControl** オブジェクトには、新しいレコードのセットが反映されます。 既存の [レコードセット](../ado-api/recordset-object-ado.md) オブジェクトがすべて解放され、保存されていない変更はすべて破棄されます。 **Refresh**メソッドでは、最初のレコードが自動的に現在のレコードになります。  
  
 データを操作するときは、 **Refresh** メソッドを定期的に呼び出すことをお勧めします。 データを取得し、しばらくの間クライアントコンピューターに残しておくと、最新の状態にならない可能性があります。 他のユーザーがレコードを変更して変更を送信した可能性があるため、変更が失敗する可能性があります。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [Refresh メソッドの例 (VB)](../ado-api/refresh-method-example-vb.md)   
 [Refresh メソッドの例 (VBScript)](./refresh-method-example-vbscript.md)   
 [アドレス帳のコマンドボタン](../../guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate メソッド (RDS)](./cancelupdate-method-rds.md)   
 [Refresh メソッド (ADO)](../ado-api/refresh-method-ado.md)   
 [SubmitChanges メソッド (RDS)](./submitchanges-method-rds.md)