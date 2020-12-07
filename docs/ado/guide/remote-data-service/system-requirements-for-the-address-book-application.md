---
description: アドレス帳アプリケーションのシステム要件
title: アドレス帳アプリケーションのシステム要件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7edd6f3c383c1563122bff053e39a372dff264b3
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722834"
---
# <a name="system-requirements-for-the-address-book-application"></a>アドレス帳アプリケーションのシステム要件
アドレス帳のサンプルアプリケーションを設定するには、次のソフトウェアとデータベースの要件を満たしている必要があります。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="software-requirements"></a>ソフトウェア要件  
 この Web アプリケーションを実行するためのサーバーコンピューターソフトウェアの要件は次のとおりです。  
  
-   Microsoft Windows NT® Server 4.0、Service Pack 3 以降、または Microsoft Windows® 2000 Server。  
  
-   Active Server ページを含む Microsoft インターネットインフォメーションサービス (IIS) バージョン3.0 以降。  
  
 この Web アプリケーションを実行するためのクライアントコンピューターソフトウェアの要件は次のとおりです。  
  
-   Microsoft Internet Explorer 4.0 以降。  
  
-   Microsoft Windows NT 4.0 Workstation または Server、Windows 2000、または Microsoft Windows 98。  
  
## <a name="database-requirements"></a>データベース要件  
 このサンプルを使用するには、次のものが必要です。  
  
-   運用中の Microsoft® SQL Server バージョン6.5 以降のデータベースサーバー。  
  
-   データベースを作成し、サンプルデータを設定する権限。  
  
-   Enterprise Manager または ISQL ユーティリティ (SQL Server 7.0 のクエリアナライザーと呼ばれます) を使用して、データが設定されたことを確認します。  
  
 権限を持っていない場合は、データベース管理者がシステムをセットアップし、データベースへのアクセス許可を付与するか、データベースをセットアップする必要があります。  
  
## <a name="see-also"></a>参照  
 [アドレス帳 SQL スクリプトの実行](./running-the-address-book-sql-script.md)   
 [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [アドレス帳のサンプル アプリケーションの実行](./running-the-address-book-sample-application.md)