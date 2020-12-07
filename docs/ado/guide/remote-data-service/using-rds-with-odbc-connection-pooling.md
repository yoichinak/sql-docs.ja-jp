---
description: RDS での ODBC 接続プールの使用
title: ODBC 接続プールを使用した RDS の使用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: rothja
ms.author: jroth
ms.openlocfilehash: b455687f6869f073a4f8cc78f5a568b4d2eb4e7e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722805"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>RDS での ODBC 接続プールの使用
ODBC データソースを使用している場合は、インターネットインフォメーションサービス (IIS) の [接続プール] オプションを使用して、クライアント負荷の高パフォーマンス処理を実現できます。 接続プールは接続のためのリソースマネージャーで、頻繁に使用される接続のオープン状態を維持します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 接続プールを有効にするには、インターネットインフォメーションサービスのドキュメントを参照してください。  
  
 接続プールを有効にすると、Microsoft インターネットインフォメーションサービスのドキュメントに記載されているように、Web サーバーに他の制限が適用される可能性があることに注意してください。  
  
 接続プールが安定し、さらにパフォーマンスが向上するようにするには、TCP/IP ソケットネットワークライブラリを使用するように Microsoft SQL Server を構成する必要があります。  
  
 そのためには、次の手順を実行する必要があります。  
  
-   TCP/IP ソケットを使用するように SQL Server コンピューターを構成します。  
  
-   TCP/IP ソケットを使用するように Web サーバーを構成します。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>TCP/IP ソケットを使用するように SQL Server コンピューターを構成する  
 SQL Server コンピューターで、SQL Server セットアッププログラムを実行して、データソースとのやり取りに TCP/IP ソケットネットワークライブラリが使用されるようにします。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>SQL Server コンピューターで TCP/IP ソケットネットワークライブラリを指定するには  
  
### <a name="in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 6.5] の順にポイントし、[SQL セットアップ] をクリックします。  
  
2.  [続行] を2回クリックします。  
  
3.  [Microsoft SQL Server オプション] ダイアログボックスで [ネットワークサポートの変更] を選択し、[続行] をクリックします。  
  
4.  [TCP/IP ソケット] チェックボックスがオンになっていることを確認し、[OK] をクリックします。  
  
5.  [続行] をクリックして完了し、セットアップを終了します。  
  
### <a name="in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 7.0] の順にポイントし、[サーバーネットワークユーティリティ] をクリックします。  
  
2.  ダイアログボックスの [全般] タブで、[追加] をクリックします。  
  
3.  [ネットワークライブラリ構成の追加] ダイアログボックスで、[TCP/IP] をクリックします。  
  
4.  [ポート番号] ボックスと [プロキシアドレス] ボックスに、ネットワーク管理者から提供されたポート番号とプロキシアドレスを入力します。  
  
5.  [OK] をクリックして完了し、セットアップを終了します。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>TCP/IP ソケットを使用するように Web サーバーを構成する  
 TCP/IP ソケットを使用するように Web サーバーを構成するには、2つのオプションがあります。 どのような操作を行うかは、すべての SQL server が Web サーバーからアクセスされるか、Web サーバーからアクセスされる特定の SQL Server のみであるかによって異なります。  
  
 すべての SQL server が Web サーバーからアクセスされる場合は、Web サーバーコンピューターで SQL Server クライアント構成ユーティリティを実行する必要があります。 次の手順では、この IIS Web サーバーから TCP/IP ソケットネットワークライブラリを使用するように構成されたすべての SQL Server 接続の既定のネットワークライブラリを変更します。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>Web サーバーを構成するには (すべての SQL server)  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 6.5] の順にポイントし、[SQL クライアント構成ユーティリティ] をクリックします。  
  
2.  [Net Library] タブをクリックします。  
  
3.  [既定のネットワーク] ボックスで、[TCP/IP ソケット] を選択します。  
  
4.  [完了] をクリックして変更を保存し、ユーティリティを終了します。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 7.0] の順にポイントし、[クライアントネットワークユーティリティ] をクリックします。  
  
2.  [General] タブをクリックします。  
  
3.  [既定のネットワークライブラリ] ボックスで、[TCP/IP] をクリックします。  
  
4.  [OK] をクリックして変更を保存し、ユーティリティを終了します。  
  
 Web サーバーから特定の SQL Server にアクセスする場合は、Web サーバーコンピューターで SQL Server クライアント構成ユーティリティを実行する必要があります。 特定の SQL Server 接続のネットワークライブラリを変更するには、次のように、Web サーバーコンピューターで SQL Server クライアントソフトウェアを構成します。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>Web サーバーを構成するには (特定の SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 6.5] の順にポイントし、[SQL クライアント構成ユーティリティ] をクリックします。  
  
2.  [詳細設定] タブをクリックします。  
  
3.  [サーバー] ボックスに、TCP/IP ソケットを使用して接続するサーバーの名前を入力します。  
  
4.  [DLL 名] ボックスで、[TCP/IP Sockets] を選択します。  
  
5.  [追加/変更] をクリックします。 このサーバーを指すすべてのデータソースで TCP/IP ソケットが使用されるようになります。  
  
6.  [Done] をクリックします。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 の場合:  
  
1.  [スタート] ボタンをクリックし、[プログラム]、[Microsoft SQL Server 7.0] の順にポイントし、[クライアント構成ユーティリティ] をクリックします。  
  
2.  [General] タブをクリックします。  
  
3.  [追加] をクリックします。  
  
4.  [サーバーの別名] ボックスにサーバーの別名を入力します。 [ネットワークライブラリ] ボックスで、[TCP/IP] をクリックします。 [コンピューター名] ボックスに、TCP/IP ソケットクライアントをリッスンするコンピューターのコンピューター名を入力します。 [ポート番号] ボックスに、SQL Server がリッスンするポートを入力します。  
  
5.  [OK] をクリックし、もう一度 [OK] をクリックしてユーティリティを終了します。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)