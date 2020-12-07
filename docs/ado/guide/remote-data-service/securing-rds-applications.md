---
description: RDS アプリケーションの保護
title: RDS アプリケーションをセキュリティで保護する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: rothja
ms.author: jroth
ms.openlocfilehash: 5dbeffea507c857aec6554a8f98096d7752fe9fc
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723089"
---
# <a name="securing-rds-applications"></a>RDS アプリケーションの保護
このトピックでは、RDS のセキュリティ情報について説明します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer のセキュリティに関する問題  
 Microsoft Internet Explorer に新しいセキュリティ拡張機能が追加されたため、一部の ADO オブジェクトおよび RDS オブジェクトは、"安全な" モード環境でのみ実行されるように制限されています。 これには、さまざまなゾーン、セキュリティレベル、制限動作、安全でない操作、カスタマイズされたセキュリティ設定など、これらの問題を認識している必要があります。  
  
## <a name="security-and-your-web-server"></a>セキュリティと Web サーバー  
 インターネット Web サーバーで [RDSServer](../../reference/rds-api/datafactory-object-rdsserver.md) オブジェクトを使用する場合は、これによってセキュリティ上のリスクが生じる可能性があることに注意してください。 有効なデータソース名 (DSN)、ユーザー ID、およびパスワード情報を取得する外部ユーザーは、そのデータソースにクエリを送信するためのページを書き込むことができます。 データソースへのアクセスをさらに制限する場合は、 **RDSServer** オブジェクト (msadcf.dll) の登録を解除して削除し、代わりに、ハードコーディングされたクエリでカスタムビジネスオブジェクトを使用する方法があります。  
  
 DataFactory オブジェクトを使用した場合のセキュリティへの影響の詳細については、Microsoft セキュリティ Web サイトの「Microsoft セキュリティ情報 MS99-025」を参照してください。  
  
## <a name="client-impersonation-and-security"></a>クライアントの偽装とセキュリティ  
 IIS Web サーバーの **パスワード認証** プロパティが Windows nt チャレンジ/レスポンス認証 (windows nt 4.0 の場合) または統合 Windows 認証 (windows 2000 の場合) に設定されている場合、ビジネスオブジェクトはクライアントのセキュリティコンテキストで呼び出されます。 これは、HTTP 経由のクライアント偽装を可能にする RDS 1.5 の新機能です。 このモードで作業している場合、Web サーバー (IIS) へのログオンは匿名ではなく、クライアントコンピューターが実行されているユーザー ID とパスワードを使用します。 ODBC Dsn が信頼関係接続を使用するように設定されている場合、SQL Server などのデータベースへのアクセスも、クライアントのセキュリティコンテキストで発生します。 ただし、これは、データベースが IIS と同じコンピューター上にある場合にのみ機能します。クライアントの資格情報を他のコンピューターに引き継ぐことはできません。  
  
 たとえば、userid = "JohnD" および password = "secret" を含むクライアント John Doe がクライアントコンピューターにログオンしているとします。 IIS を実行している "MyServer" コンピューターで SQL クエリを実行することで、 **DataFactory** オブジェクトにアクセスして [レコードセット](../../reference/ado-api/recordset-object-ado.md) を作成する必要があるブラウザーベースのアプリケーションを実行します。 Windows NT Server 4.0 を実行しているシステムである MyServer は、Windows NT チャレンジ/レスポンス認証を使用するように設定されています。 ODBC DSN では、[信頼できる接続を使用する] が選択されています。また、サーバーにも SQL Server データソースが含まれています。 Web サーバーで要求が受信されると、クライアントにユーザー ID とパスワードの入力が求められます。 このため、要求は、IUSER_MyServer ではなく "JohnD"/"Secret" (匿名パスワード認証がオンになっている場合の既定値) として MyServer に記録されます。 同様に、SQL Server にログオンすると、"JohnD"/"Secret" が使用されます。  
  
 このため、IIS の Windows NT チャレンジ/レスポンス認証モードでは、ユーザーがデータベースにログオンするために必要なユーザー ID とパスワードの情報を明示的に要求しなくても、HTML ページを作成できます。 IIS の基本認証が使用されている場合は、これも必要になります。  
  
## <a name="password-authentication"></a>パスワード認証  
 RDS は、匿名、基本、または NT チャレンジ/レスポンス認証 (Windows 2000 では統合 Windows 認証と呼ばれます) の3つのパスワード認証モードのいずれかで実行されている IIS Web サーバーと通信できます。 これらの設定は、Web サーバーがアクセスを制御する方法を定義します。たとえば、クライアントコンピューターに NT Web サーバー上での明示的なアクセス特権が必要になります。