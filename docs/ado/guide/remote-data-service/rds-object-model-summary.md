---
description: RDS オブジェクト モデルの概要
title: RDS オブジェクトモデルの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 456bfdf7e41b10c4a42708eabb21b485de463ca7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721423"
---
# <a name="rds-object-model-summary"></a>RDS オブジェクト モデルの概要
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
|Object|説明|  
|------------|-----------------|  
|[RDS.DataSpace](../../reference/rds-api/dataspace-object-rds.md)|このオブジェクトには、サーバープロキシを取得するメソッドが含まれています。 既定のプロキシまたはカスタムサーバープログラム (ビジネスオブジェクト) を指定できます。 サーバープログラムは、インターネット、イントラネット、ローカルエリアネットワーク、またはローカルダイナミックリンクライブラリで呼び出すことができます。<br /><br /> オブジェクト **スペース** オブジェクトは、スクリプト作成には安全です。|  
|[RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)|このオブジェクトは、既定のサーバープログラムを表します。 RDS のデータの取得と更新の既定の動作を実行します。<br /><br /> **DataFactory**オブジェクトは、スクリプト作成には安全ではありません。|  
|[RDS.DataControl](../../reference/rds-api/datacontrol-object-rds.md)|このオブジェクトは、RDS を自動的に呼び出すことができ **ます。RDSServer オブジェクトと** **DataFactory** オブジェクト。<br /><br /> このオブジェクトを使用して、RDS データの既定の取得または更新動作を呼び出します。<br /><br /> このオブジェクトには、返された **レコードセット** オブジェクトにアクセスするためのビジュアルコントロールの手段も用意されています。<br /><br /> **DataControl**オブジェクトは、スクリプト作成には安全です。|  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)   
 [RDS のシナリオ](./rds-scenario.md)   
 [RDS チュートリアル](./rds-tutorial.md)   
 [RDS の使用方法とセキュリティ](./rds-usage-and-security.md)