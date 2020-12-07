---
description: RDS プロパティ
title: RDS のプロパティ |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS properties [ADO]
- properties [ADO], RDS
ms.assetid: e4e04cbd-21fc-44a1-9f21-49aa68746934
author: rothja
ms.author: jroth
ms.openlocfilehash: 75124c0fc8d7a0c3c0bb0ea491c84c3673339108
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724353"
---
# <a name="rds-properties"></a>RDS プロパティ
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
|プロパティ|説明|  
|-|-|  
|[接続 (RDS)](./connect-property-rds.md)|クエリおよび更新操作の実行元のデータベース名を示します。|  
|[ExecuteOptions (RDS)](./executeoptions-property-rds.md)|非同期実行が有効かどうかを示します。|  
|[FetchOptions (RDS)](./fetchoptions-property-rds.md)|非同期フェッチの種類を示します。|  
|[FilterColumn (RDS)](./filtercolumn-property-rds.md)|フィルター条件を評価する列を示します。|  
|[FilterCriterion (RDS)](./filtercriterion-property-rds.md)|フィルター値に使用する評価演算子を示します。|  
|[FilterValue (RDS)](./filtervalue-property-rds.md)|レコードをフィルター処理するための値を示します。|  
|[ハンドラー (RDS)](./handler-property-rds.md)|**RDSServer**の機能を拡張するサーバー側のカスタマイズプログラム (*ハンドラー*) の名前と、*ハンドラー*によって使用されるすべてのパラメーターを示します。|  
|[InternetTimeout (RDS)](./internettimeout-property-rds.md)|要求がタイムアウトするまでのミリ秒単位の待機時間を示します。|  
|[ReadyState (RDS)](./readystate-property-rds.md)|**DataControl**オブジェクトが**レコードセット**オブジェクトにデータをフェッチする際の進行状況を示します。|  
|[Recordset と SourceRecordset (RDS)](./recordset-sourcerecordset-properties-rds.md)|カスタムビジネスオブジェクトから返される **レコードセット** オブジェクトを示します。|  
|[サーバー (RDS)](./server-property-rds.md)|インターネットインフォメーションサービス (IIS) 名と通信プロトコルを示します。|  
|[SortColumn (RDS)](./sortcolumn-property-rds.md)|レコードを並べ替える列を指定します。|  
|[SortDirection (RDS)](./sortdirection-property-rds.md)|並べ替え順序が昇順と降順のどちらであるかを示します。|  
|[SQL (RDS)](./sql-property.md)|**レコードセット**を取得するために使用するクエリ文字列を示します。|  
|[URL (RDS)](./url-property-rds.md)|相対 URL または絶対 URL を含む文字列を示します。|