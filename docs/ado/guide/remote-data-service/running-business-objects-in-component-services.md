---
description: コンポーネント サービスでのビジネス オブジェクトの実行
title: コンポーネントサービスでのビジネスオブジェクトの実行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e4cafeaf590c07ec52153a2932de3e105e26950
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723103"
---
# <a name="running-business-objects-in-component-services"></a>コンポーネント サービスでのビジネス オブジェクトの実行
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 ビジネスオブジェクトには、実行可能ファイル (.exe) またはダイナミックリンクライブラリ (.dll) を指定できます。 ビジネスオブジェクトの実行に使用する構成は、オブジェクトが .dll または .exe ファイルのどちらであるかによって異なります。  
  
-   .Exe ファイルとして作成されたビジネスオブジェクトは、DCOM を介して呼び出すことができます。 これらのビジネスオブジェクトがインターネットインフォメーションサービス (IIS) で使用されている場合は、データの追加のマーシャリングによって、クライアントのパフォーマンスが低下する可能性があります。  
  
-   .Dll ファイルとして作成されたビジネスオブジェクトは、IIS を介して使用することも、HTTP で使用することもできます。 また、Windows NT を使用している場合は、コンポーネントサービスまたは Microsoft トランザクションサーバーを介して DCOM 経由でのみ使用できます。 IIS を使用してアクセスするには、ビジネスオブジェクト Dll を IIS サーバーコンピューターに登録する必要があります。 DLL を DCOM 上で実行するように構成する方法の詳細については、「 [dcom を有効](./enabling-a-dll-to-run-on-dcom.md)にする」セクションを参照してください。  
  
> [!NOTE]
>  中間層のビジネスオブジェクトが **Getobjectcontext**、 **SetComplete**、および **SetAbort**を使用してコンポーネントサービスコンポーネントとして実装されている場合、ビジネスオブジェクトはコンポーネントサービス (Windows NT を使用している場合は MTS) を使用して、複数のクライアント呼び出しで状態を維持することができます。 このシナリオは、通常、信頼されたクライアントとイントラネット内のサーバーの間で実装される DCOM で実現できます。 この例では、 [RDS です。](../../reference/rds-api/dataspace-object-rds.md) クライアント側の領域スペースオブジェクトと [CreateObject](../../reference/rds-api/createobject-method-rds.md) メソッドは、トランザクションコンテキストオブジェクトと **CreateInstance** メソッドに置き換えられます。このメソッドは、 **ITransactionContext** インターフェイスによって提供され、コンポーネントサービスによって実装されます。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)