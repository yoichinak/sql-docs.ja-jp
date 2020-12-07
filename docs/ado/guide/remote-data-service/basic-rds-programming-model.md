---
description: RDS の基本プログラミング モデル
title: 基本的な RDS プログラミングモデル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: rothja
ms.author: jroth
ms.openlocfilehash: b43d18127717ae58b4db2c8fb33c5d173ab160af
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724833"
---
# <a name="basic-rds-programming-model"></a>RDS の基本プログラミング モデル
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 RDS は、次の環境に存在するアプリケーションに対応します。クライアントアプリケーションは、サーバー上で実行されるプログラムと、目的の情報を返すために必要なパラメーターを指定します。 サーバーで呼び出されたプログラムは、指定されたデータソースへのアクセス権を取得し、情報を取得し、必要に応じてデータを処理してから、結果の情報をクライアントアプリケーションに返します。この形式は、簡単に使用できます。 RDS には、次の一連の操作を実行するための手段が用意されています。  
  
-   サーバーで呼び出されるプログラムを指定し、クライアントからそのプログラムを参照する方法を取得します。 (この参照は *プロキシ*と呼ばれることもあります。 リモートサーバープログラムを表します。 クライアントアプリケーションは、ローカルプログラムのようにプロキシを "呼び出す" としますが、実際にはリモートサーバープログラムを呼び出します)。  
  
-   サーバープログラムを起動します。 データソースと発行するコマンドを識別するパラメーターをサーバープログラムに渡します。 (サーバープログラムは実際には ADO を使用してデータソースにアクセスします。 ADO は、指定されたパラメーターのいずれかと接続を確立し、もう一方のパラメーターで指定されたコマンドを発行します。  
  
-   サーバープログラムは、データソースから [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを取得します。 必要に応じて、 **レコードセット** オブジェクトがサーバー上で処理されます。  
  
-   サーバープログラムによって、最終的な **レコードセット** オブジェクトがクライアントアプリケーションに返されます。  
  
-   クライアントでは、 **レコードセット** オブジェクトは、ビジュアルコントロールで簡単に使用できるフォームに配置されます。  
  
-   **Recordset**オブジェクトに対する変更は、サーバープログラムに送り返されます。このオブジェクトを使用してデータソースを更新します。  
  
 このプログラミングモデルには、便利な機能がいくつか含まれています。 複雑なサーバープログラムを使用してデータソースにアクセスする必要がなく、必要な接続パラメーターとコマンドパラメーターを指定した場合、RDS は、単純な既定のサーバープログラムを使用して、指定されたデータを自動的に取得します。  
  
 より複雑な処理が必要な場合は、独自のカスタムサーバープログラムを指定できます。 たとえば、カスタムサーバープログラムは ADO の完全な機能を備えているため、さまざまなデータソースに接続して、データを複雑な方法で結合し、単純な処理結果をクライアントアプリケーションに返すことができます。  
  
 最後に、必要な場所がどこかにある場合、ADO では、既定のサーバープログラムの動作のカスタマイズがサポートされるようになりました。  
  
## <a name="see-also"></a>参照  
 [RDS プログラミングモデルの詳細](./rds-programming-model-in-detail.md)   
 [RDS のシナリオ](./rds-scenario.md)   
 [RDS チュートリアル](./rds-tutorial.md)   
 [Recordset オブジェクト (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [RDS の使用方法とセキュリティ](./rds-usage-and-security.md)