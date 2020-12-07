---
description: RDS のシナリオ
title: RDS のシナリオ |Microsoft Docs
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
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c9b7563b940cd4340b7f07238fe50af56cf66e6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721413"
---
# <a name="rds-scenario"></a>RDS のシナリオ
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 アドレス帳アプリケーションは、リモートデータサービス (RDS) を使用して単純なデータ対応 Web アプリケーションを構築する方法を示すシナリオです (オンラインの企業アドレス帳)。 このシナリオは、データ対応の ActiveX コントロールを RDS で使用する方法や、データ中心の Web アプリケーションを構築する経験豊富なソフトウェア開発者を対象とする Microsoft Visual Basic Scripting Edition (VBScript) および COM プログラマに役立ちます。  
  
 このシナリオでは、基本的な HTML レイアウトタグを使用する方法、DHTML データバインディング技法を使用する方法、および ActiveX コントロールでプログラミングする方法を理解していることを前提としています。  
  
 SDK がインストールされている場合、アドレス帳サンプルアプリケーションの完全なソースコードは、samples\dataaccess\rds\AddressBook\AddressBook.asp. の SDK ディレクトリにあります。 アドレス帳のシナリオを表示するには、Internet Explorer 4.0 以降で、「 **https://*webserver*/RDS/AddressBook/AddressBook.asp** 」と入力します *。ここで、web サーバー* には、インターネットインフォメーションサービス (IIS) および Asp を実行している windows NT 4.0 または windows 2000 Web サーバーコンピューターの名前を指定します。  
  
## <a name="introduction-to-address-book"></a>アドレス帳の概要  
 アドレス帳のサンプルアプリケーションには、検索可能なディレクトリをイントラネット経由で公開するために使用できる単純なオンラインアドレス帳が用意されています。 アドレス帳は、ユーザーが1つまたは複数のフィールドに検索文字列を入力して、従業員に関する情報を要求できるように設計されています。 リモートデータサービスの基本的な機能を紹介するために、サンプルアプリケーションは、最小数のオブジェクトと検索フィールドを使用して意図的に小さく保持されています。  
  
 アプリケーションインターフェイスは、次の部分で構成されています。  
  
-   非ビジュアル **RDS。DataControl** は、データベースに接続するためにクライアントによって使用されるデータバインドオブジェクトです。  
  
-   Employee 属性検索条件の入力フィールドとして機能する HTML テキストボックス。  
  
-   クエリの作成、検索フィールドのクリア、従業員情報を使用したデータベースの更新、保留中の変更の取り消し、およびグリッドに表示されているデータ行の移動を行うための HTML コマンドボタン。  
  
-   バックエンドデータベースに対するクエリから返されたデータを表示するための DHTML データバインディング (RDS を介して) **。DataControl** テーブル内のデータバインディングオブジェクト)。  
  
-   前に説明した各要素に接続して対話できるようにする VBScript ルーチン。 VBScript コードは、RDS を初期化するためにも使用され **ます。DataControl** オブジェクトを作成し、RDS の名前から HTML テーブルの列見出しを動的に作成し **ます。DataControl** レコードセットフィールド。  
  
 ステップごとのリンクに従って、シナリオを設定して実行し、シナリオの動作の詳細を確認してください。  
  
 このシナリオには、次のトピックが含まれています。  
  
-   [アドレス帳アプリケーションのシステム要件](./system-requirements-for-the-address-book-application.md)  
  
-   [アドレス帳の SQL スクリプトの実行](./running-the-address-book-sql-script.md)  
  
-   [アドレス帳のサンプル アプリケーションの実行](./running-the-address-book-sample-application.md)  
  
-   [アドレス帳のデータ バインディング オブジェクト](./address-book-data-binding-object.md)  
  
-   [アドレス帳のコマンド ボタン](./address-book-command-buttons.md)  
  
-   [アドレス帳のナビゲーション ボタン](./address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>参照  
 [アドレス帳アプリケーションのシステム要件](./system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX データオブジェクト (ADO)](../../microsoft-activex-data-objects-ado.md)   
 [RDS の基礎](./rds-fundamentals.md)   
 [RDS チュートリアル](./rds-tutorial.md)