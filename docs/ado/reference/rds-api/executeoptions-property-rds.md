---
description: ExecuteOptions プロパティ (RDS)
title: ExecuteOptions プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fe38de33ea0b5f0784af27f031d2a93759d15aa
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722358"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions プロパティ (RDS)
非同期実行が有効かどうかを示します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 次のいずれかの値を設定または返します。  
  
|定数|説明|  
|--------------|-----------------|  
|**adcExecSync**|[レコードセット](../ado-api/recordset-object-ado.md)の次の更新を同期的に実行します。|  
|**adcExecAsync**|既定値。 **レコードセット**の次の更新を非同期的に実行します。|  
  
> [!NOTE]
>  これらの定数を使用する実行可能ファイルはそれぞれ、それぞれの宣言を提供する必要があります。 RDS ライブラリの既定のインストールフォルダーにある Adcvbs. inc. ファイルから、必要な定数宣言を切り取って貼り付けることができます。  
  
## <a name="remarks"></a>解説  
 **Executeoptions**が**Adcexecasync**に設定されている場合、RDS で次の**更新**呼び出しが非同期に実行され[ます。DataControl](./datacontrol-object-rds.md)オブジェクトの**レコードセット**。  
  
 RDS を変更する可能性のある別の非同期操作中に [Reset](./reset-method-rds.md)、 [Refresh](./refresh-method-rds.md)、 [SubmitChanges](./submitchanges-method-rds.md)、 [CancelUpdate](../ado-api/cancelupdate-method-ado.md)、または [レコードセット](./recordset-sourcerecordset-properties-rds.md) を呼び出そうとした場合 [。DataControl](./datacontrol-object-rds.md) オブジェクトの **レコードセット** が実行中であるため、エラーが発生します。  
  
 非同期操作中にエラーが発生した場合は、 **RDS.DataControl** オブジェクトの [ReadyState](./readystate-property-rds.md) 値が **Adcreadystateloaded** から **adcReadyStateComplete**に変更されましたが、 **レコードセット** プロパティの値は *何も*保持されません。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [ExecuteOptions および FetchOptions プロパティの例 (VBScript)](./executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel メソッド (RDS)](./cancel-method-rds.md)