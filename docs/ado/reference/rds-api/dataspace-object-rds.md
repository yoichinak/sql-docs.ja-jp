---
description: DataSpace オブジェクト (RDS)
title: 領域スペースオブジェクト (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: rothja
ms.author: jroth
ms.openlocfilehash: e30697dd8b751ec3122683a792a242e6faa0fff0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720853"
---
# <a name="dataspace-object-rds"></a>DataSpace オブジェクト (RDS)
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 は、中間層に配置されているカスタムビジネスオブジェクトに対してクライアント側プロキシを作成します。  
  
 リモートデータサービスでは、クライアント側コンポーネントが中間層に配置されているビジネスオブジェクトと通信できるように、ビジネスオブジェクトプロキシが必要です。 プロキシは、プロセスまたはコンピューターの境界を越えて、アプリケーションの [レコードセット](../ado-api/recordset-object-ado.md) データのパッケージ化、unpackaging、および転送 (マーシャリング) を容易にします。  
  
 リモートデータサービスは RDS を使用 **します。** ビジネスオブジェクトプロキシを作成するための、領域スペースオブジェクトの [CreateObject](./createobject-method-rds.md) メソッド。 ビジネスオブジェクトプロキシは、対応する中間層ビジネスオブジェクトのインスタンスが作成されるたびに動的に作成されます。 リモートデータサービスは、HTTP、HTTPS (HTTP Secure Sockets)、DCOM、およびインプロセス (クライアントコンポーネントとビジネスオブジェクトが同じコンピューターに存在する) のプロトコルをサポートしています。  
  
> [!NOTE]
>  Rds は、Rds が "ステートレス" な方法で動作 **します。領域間オブジェクトは** 、HTTP または HTTPS プロトコルを使用します。 つまり、サーバーが応答を返すと、クライアント要求に関する内部情報は破棄されます。  
  
> [!NOTE]
>  ビジネスオブジェクトは、ビジネスオブジェクトプロキシの有効期間中は存在するように見えますが、ビジネスオブジェクトが実際に存在するのは、要求に応答が送信されるまでの間だけです。 要求が発行されると (つまり、ビジネスオブジェクトでメソッドが呼び出されると)、プロキシはサーバーへの新しい接続を開き、サーバーはビジネスオブジェクトの新しいインスタンスを作成します。 ビジネスオブジェクトが要求に応答すると、サーバーはビジネスオブジェクトを破棄し、接続を閉じます。  
  
> [!NOTE]
>  この動作は、ビジネスオブジェクトのプロパティまたは変数を使用して、ある要求から別の要求にデータを渡すことができないことを意味します。 状態データを永続化するには、ファイルやメソッドの引数など、他のメカニズムを使用する必要があります。  
  
 RDS のクラス ID **。領域スペース** オブジェクトは BD96C556-65A3-11D0-983A-00C04FC29E36 です。  
  
 オブジェクト **スペース** オブジェクトは、スクリプト作成には安全です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [DataSpace オブジェクト (RDS) のプロパティ、メソッド、およびイベント](./dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [DataSpace オブジェクトおよび CreateObject メソッドの例 (VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)