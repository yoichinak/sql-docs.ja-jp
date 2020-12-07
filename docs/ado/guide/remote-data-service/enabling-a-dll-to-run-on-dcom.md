---
description: DCOM 上で実行するための DLL の有効化
title: DLL を DCOM で実行できるようにする |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: rothja
ms.author: jroth
ms.openlocfilehash: 220f4a8abfe37a12a7f0699b9aec8a634691cabe
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723223"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>DCOM 上で実行するための DLL の有効化
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 次の手順では、ビジネスオブジェクトの .dll で、コンポーネントサービスを介して DCOM と Microsoft インターネットインフォメーションサービス (HTTP) の両方を使用できるようにする方法を説明します。  
  
1.  コンポーネントサービス MMC スナップインで、新しい空のパッケージを作成します。  
  
     コンポーネントサービス MMC スナップインを使用して、パッケージを作成し、このパッケージに DLL を追加します。 これにより、DCOM を介して .dll にアクセスできるようになりますが、IIS を使用してユーザー補助が削除されます。 (レジストリで .dll をチェックインすると、 **inproc** キーは空になります。このトピックの後半で説明する Activation 属性を設定すると、 **inproc** キーに値が追加されます)。  
  
2.  ビジネスオブジェクトをパッケージにインストールします。  
  
     または  
  
     パッケージに [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) オブジェクトをインポートします。  
  
3.  **作成者のプロセス**(ライブラリアプリケーション) で、パッケージの [アクティブ化] 属性をに設定します。  
  
     同じコンピューターで DCOM と IIS を使用して .dll にアクセスできるようにするには、コンポーネントサービス MMC スナップインでコンポーネントのアクティブ化属性を設定する必要があります。 **作成者のプロセスで**属性をに設定すると、コンポーネントサービスのサロゲート .dll を指す**Inproc**サーバーキーがレジストリに追加されていることがわかります。  
  
 コンポーネントサービス (または Microsoft トランザクションサービス) の詳細、およびこれらの手順の実行方法については、Microsoft トランザクションサーバーの Web サイトを参照してください。