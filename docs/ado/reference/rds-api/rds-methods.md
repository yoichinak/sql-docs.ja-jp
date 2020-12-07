---
description: RDS メソッド
title: RDS のメソッド |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: f65c669a12fce6b78572e2bacd3152cdb5793216
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724363"
---
# <a name="rds-methods"></a>RDS メソッド
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
|Method|説明|  
|-|-|  
|[キャンセル (RDS)](./cancel-method-rds.md)|保留中の非同期メソッド呼び出しの実行を取り消します。|  
|[CancelUpdate (RDS)](./cancelupdate-method-rds.md)|**Recordset**オブジェクトの現在の行または新しい行に対して行われたすべての変更を取り消します。|  
|[ConvertToString (RDS)](./converttostring-method-rds.md)|レコードセットを、レコードセットデータを表す MIME **文字列に変換** します。|  
|[CreateObject (RDS)](./createobject-method-rds.md)|対象のビジネスオブジェクトのプロキシを作成し、そのオブジェクトへのポインターを返します。|  
|[CreateRecordset (RDS)](./createrecordset-method-rds.md)|空の非接続 **レコードセット**を作成します。|  
|[Execute メソッド (RDS)](./execute-method-rds.md)|要求を実行し、高度なデータ行セットを作成します (ADO 2.5 以降で使用)。|  
|[Execute21 メソッド (RDS)](./execute21-method-rds.md)|要求を実行し、高度なデータ行セットを作成します (ADO 2.1 で使用)。|  
|[InvokeService (RDS)](./invokeservice-rds.md)|サポートされているオブジェクトのバージョンで、要求されたインターフェイスへのポインターを返します。|  
|[MoveFirst、MoveLast、MoveNext、MovePrevious (RDS)](./movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|指定された **レコードセット** オブジェクト内の最初、最後、次、または前のレコードに移動します。|  
|[クエリ (RDS)](./query-method-rds.md)|は、有効な SQL クエリ文字列を使用して **レコードセット**を返します。|  
|[更新 (RDS)](./refresh-method-rds.md)|**接続**プロパティで指定されたデータソースを再クエリし、クエリ結果を更新します。|  
|[リセット (RDS)](./reset-method-rds.md)|指定された並べ替えとフィルターのプロパティに基づいて、クライアント側の **レコードセット**に対して並べ替えまたはフィルター処理を実行します。|  
|[SubmitChanges (RDS)](./submitchanges-method-rds.md)|ローカルにキャッシュされたレコードセットと更新可能な **レコードセット** の保留中の変更を **接続** プロパティで指定されたデータソースに送信します。|  
|[Synchronize メソッド (RDS)](./synchronize-method-rds.md)|接続文字列で指定されたデータベースと、指定されたレコードセットを同期します (ADO 2.5 以降で使用)。|  
|[Synchronize21 メソッド (RDS)](./synchronize21-method-rds.md)|接続文字列で指定されたデータベースと、指定されたレコードセットを同期します (ADO 2.1 で使用)。|