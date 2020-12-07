---
description: アドレス帳の SQL スクリプトの実行
title: アドレス帳 SQL スクリプトの実行 |Microsoft Docs
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
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: rothja
ms.author: jroth
ms.openlocfilehash: 0550e12f67538e9872797031146a34c83a0ec87f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721363"
---
# <a name="running-the-address-book-sql-script"></a>アドレス帳の SQL スクリプトの実行
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 次のような、ISQL/Query Analyzer コマンドラインユーティリティまたは SQL Server Enterprise マネージャーを使用して、含まれている SQL スクリプト (Sampleemp .sql) を実行する必要があります。  
  
-   新しいデータベース (AddrBookDB) を既定のデバイスに作成します。  
  
-   データベース (AddrBookDB) に接続します。  
  
-   Employee テーブルを作成します。  
  
-   テーブルにサンプルデータを設定します。  
  
-   単純な SELECT ステートメントを実行して、データベーステーブルの作成を検証します。  
  
-   "Adcdemo" というパスワードを使用して、"adcdemo" という名前のユーザーアカウントを設定します。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 で Sampleemp .sql スクリプトを実行するには  
  
1.  [ **スタート**] をクリックし、[ **プログラム**] をポイントして、[ **Microsoft SQL Server 6.5**] をポイントします。 [ **SQL Enterprise Manager**] をクリックします。  
  
2.  [ **ツール** ] メニューの [ **SQL クエリツール**] をクリックします。  
  
3.  [ **SQL スクリプトの読み込み** ] をクリックし、C:\ Platform SDK\Samples\DataAccess\RDS\AddressBook. を参照します。  
  
4.  ファイル [Sampleemp .sql] を選択します。 **[開く]** をクリックします。  
  
5.  [ **クエリの実行** ] ボタン (ツールバーの緑色の矢印) をクリックします。  
  
6.  実行した後、 **クエリ** と **Enterprise Manager** ウィンドウを閉じます。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 で Sampleemp .sql スクリプトを実行するには  
  
1.  [ **スタート**] をクリックし、[ **プログラム**] をポイントして、[ **Microsoft SQL Server 7.0**] をポイントします。 [ **Enterprise Manager**] をクリックします。  
  
2.  使用する SQL Server が、Enterprise Manager の登録済みサーバーの一覧から選択されていることを確認してください。  
  
3.  [ **ツール** ] メニューの [ **クエリアナライザーの SQL Server**] をクリックします。  
  
4.  [ **SQL スクリプトの読み込み** ] ボタン (ツールバーの [フォルダーを開く]) をクリックし、C:\ Platform SDK\Samples\DataAccess\RDS\AddressBook. を参照します。  
  
5.  ファイル [Sampleemp .sql] を選択します。 **[開く]** をクリックします。  
  
6.  [ **クエリの実行** ] ボタン (ツールバーの緑色の矢印) または **F5 キー**をクリックします。  
  
7.  実行後、 **クエリ**、 **クエリアナライザー**、および **Enterprise Manager** ウィンドウを閉じます。  
  
## <a name="see-also"></a>参照  
 [アドレス帳のサンプル アプリケーションの実行](./running-the-address-book-sample-application.md)