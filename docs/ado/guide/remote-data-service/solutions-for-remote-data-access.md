---
description: リモート データ アクセスのソリューション
title: リモートデータアクセスのソリューション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e46994321b73166095acbb0891f5434a6fc86a1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723041"
---
# <a name="solutions-for-remote-data-access"></a>リモート データ アクセスのソリューション
## <a name="the-issue"></a>問題  
 ADO を使用すると、アプリケーションはデータソースに直接アクセスし、変更することができます (2 層システムと呼ばれることもあります)。 たとえば、データが格納されているデータソースへの接続である場合、これは2層システムで直接接続されます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 ただし、Microsoft®インターネットインフォメーションサービス (IIS) などの中継局を介して間接的にデータソースにアクセスすることもできます。 この配置は、3層システムと呼ばれることもあります。 IIS は、ローカルまたはクライアントのアプリケーションがインターネットまたはイントラネット経由でリモートまたはサーバーのプログラムを呼び出すための効率的な方法を提供するクライアント/サーバーシステムです。 サーバープログラムは、データソースへのアクセスを取得し、必要に応じて取得したデータを処理します。  
  
 たとえば、イントラネット Web ページには、Microsoft® Visual Basic Scripting Edition (VBScript) で記述されたアプリケーションが含まれています。このアプリケーションは IIS に接続します。 次に、IIS は実際のデータソースに接続し、データを取得して何らかの方法で処理した後、処理された情報をアプリケーションに返します。  
  
 この例では、アプリケーションはデータソースに直接接続されていません。IIS が失敗しました。 IIS は ADO によってデータにアクセスします。  
  
> [!NOTE]
>  クライアント/サーバーアプリケーションは、インターネットまたはイントラネットに基づく必要はありません (つまり、Web ベース)。ローカルエリアネットワーク上のコンパイルされたプログラムだけで構成される可能性があります。 ただし、一般的なケースは、Web ベースのアプリケーションです。  
  
 グリッド、チェックボックス、一覧などのビジュアルコントロールは、返された情報を使用する場合があるため、ビジュアルコントロールで返される情報を簡単に使用できるようにする必要があります。  
  
 3層システムをサポートする単純で効率的なアプリケーションプログラミングインターフェイスが必要であり、2層システムで取得された場合と同じように簡単に情報を返します。 リモートデータサービス (RDS) は、このインターフェイスです。  
  
## <a name="the-solution"></a>解決策  
 RDS は、データソースへのアクセスと更新を取得するために必要なアクティビティのシーケンスを定義します。このモデルでは、インターネットインフォメーションサービス (IIS) などの中継局を介してデータにアクセスできます。 プログラミングモデルは、RDS の機能全体をまとめたものです。  
  
## <a name="see-also"></a>参照  
 [基本的な RDS プログラミングモデル](./basic-rds-programming-model.md)   
 [RDS のシナリオ](./rds-scenario.md)   
 [RDS チュートリアル](./rds-tutorial.md)   
 [RDS の使用方法とセキュリティ](./rds-usage-and-security.md)