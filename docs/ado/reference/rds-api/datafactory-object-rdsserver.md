---
description: DataFactory オブジェクト (RDSServer)
title: DataFactory オブジェクト (RDSServer) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e31d39f0820a485d4954d789fe2dfb398d8490b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720983"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory オブジェクト (RDSServer)
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 この既定のサーバー側ビジネスオブジェクトは、クライアント側アプリケーションの指定されたデータソースへの読み取り/書き込みデータアクセスを提供するメソッドを実装します。  
  
 RDSServer オブジェクトは、クライアント要求を受け取るサーバー側オートメーションオブジェクトとして設計されてい **ます** 。 インターネット実装では、Web サーバー上に存在し、ADISAPI コンポーネントによってインスタンス化されます。 **RDSServer**オブジェクトは、指定されたデータソースへの読み取りおよび書き込みアクセスを提供しますが、検証やビジネスルールのロジックは含まれません。  
  
 **RDSServer DataFactory**と RDS の両方で使用できるメソッドを使用する場合[。DataControl](./datacontrol-object-rds.md)オブジェクトでは、リモートデータサービスは RDS を使用し**ます。** 既定で DataControl バージョン。 既定では、基本的なプログラミングシナリオが想定されています。ここでは、 **RDSServer** が汎用的なサーバー側ビジネスオブジェクトとして機能します。  
  
 Web アプリケーションでタスク固有のサーバー側の処理を処理する場合は、 **RDSServer DataFactory** をカスタムビジネスオブジェクトに置き換えることができます。  
  
 [クエリ](./query-method-rds.md)や[CreateRecordset](./createrecordset-method-rds.md)などの**DataFactory**メソッドを呼び出すサーバー側ビジネスオブジェクトを作成できます。 これは、ビジネスオブジェクトに機能を追加するが、既存のリモートデータサービステクノロジを利用する場合に便利です。  
  
 **DataFactory**オブジェクトは、クライアント側で実行されるスクリプトに対して安全ではありません。  
  
 **DataFactory**オブジェクトのクラス ID は9381D8F5-0288-11D0-9501-00AA00B911A5 です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [DataFactory オブジェクト (RDSServer) のプロパティ、メソッド、およびイベント](./datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [DataFactory オブジェクト、Query メソッド、および CreateObject メソッドの例 (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)