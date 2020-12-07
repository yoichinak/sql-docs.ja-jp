---
description: CreateObject メソッド (RDS)
title: CreateObject メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: rothja
ms.author: jroth
ms.openlocfilehash: ae158d217437184be4ead71beeb2d2404248396f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722438"
---
# <a name="createobject-method-rds"></a>CreateObject メソッド (RDS)
対象のビジネスオブジェクトのプロキシを作成し、そのオブジェクトへのポインターを返します。 プロキシは、ビジネスオブジェクトとの通信のためにデータをパッケージ化してサーバー側スタブにマーシャリングし、インターネット経由で要求とデータを送信します。 インプロセスコンポーネントオブジェクトの場合、プロキシは使用されません。オブジェクトへのポインターだけが使用されます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
 リモートデータサービスは、HTTP、HTTPS (Secure Socket Layer 経由の HTTP)、DCOM、およびインプロセスの各プロトコルをサポートしています。  
  
|Protocol|構文|  
|--------------|------------|  
|HTTP|Set object = の場合は、CreateObject. CreateObject ("ProgId", "https/ \: websrvr")|  
|HTTPS|Set object = の場合は、CreateObject. CreateObject ("ProgId", "https/ \: websrvr")|  
|DCOM|Set object = の場合は、CreateObject. CreateObject ("ProgId", "computername")|  
|インプロセス|Set object = を設定します。 CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>パラメーター  
 *Object*  
 *ProgID*で指定された型のオブジェクトに評価されるオブジェクト変数。  
  
 *DataSpace*  
 RDS を表すオブジェクト変数です [。新しいオブジェクトの](./dataspace-object-rds.md) インスタンスを作成するために使用される、領域内のオブジェクト。  
  
 *ProgID*  
 アプリケーションのビジネスルールを実装するサーバー側ビジネスオブジェクトを指定するプログラム識別子を含む **文字列** 値です。  
  
 *awebsrvr* または *computername*  
 サーバービジネスオブジェクトのインスタンスが作成されるインターネットインフォメーションサービス (IIS) Web サーバーを識別する URL を表す **文字列** 値です。  
  
## <a name="remarks"></a>解説  
 *HTTP プロトコル*は標準の Web プロトコルです。*HTTPS*はセキュリティで保護された Web プロトコルです。 HTTP を使用せずにローカルエリアネットワークを実行する場合は、 *DCOM プロトコル* を使用します。 *インプロセス*プロトコルは、ローカルダイナミックリンクライブラリ (DLL) です。ネットワークを使用しません。  
  
## <a name="applies-to"></a>適用対象  
 [DataSpace オブジェクト (RDS)](./dataspace-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [DataFactory Object、Query メソッド、および CreateObject メソッドの例 (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [領域スペースオブジェクトと CreateObject メソッドの例 (VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset メソッド (RDS)](./createrecordset-method-rds.md)