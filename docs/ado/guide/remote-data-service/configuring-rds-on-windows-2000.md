---
description: Windows 2000 での RDS の構成
title: Windows 2000 での RDS の構成 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c52989f83608b33756ae90778485bfddab08173
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724803"
---
# <a name="configuring-rds-on-windows-2000"></a>Windows 2000 での RDS の構成
Windows 2000 にアップグレードした後に RDS を正常に機能させることが困難な場合は、次の手順に従って問題のトラブルシューティングを行ってください。  
  
1.  Internet Explorer を使用して https://server に移動し、最初に World Wide Web Publishing Service が実行されていることを確認します。 この方法で Web サーバーにアクセスできない場合は、コマンドプロンプトを開き、次のコマンド "NET START W3SVC" を入力します。  
  
2.  [スタート] メニューで、[実行] を選択します。 「msdfmap.ini」と入力し、[OK] をクリックして、メモ帳で msdfmap.ini ファイルを開きます。 [CONNECT DEFAULT] セクションを確認し、ACCESS パラメーターが NOACCESS に設定されている場合は、[READONLY] に変更します。  
  
3.  RegEdit ユーティリティを使用して、"HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DataFactory\HandlerInfo" に移動し、 **ハンドラ required** が0に設定されていて、 **defaulthandler** が "" (Null 文字列) に設定されていることを確認します。  
  
     **メモ** レジストリのこのセクションに変更を加える場合は、コマンドプロンプトで次のコマンドを入力して、World Wide Web 公開サービスを停止して再起動する必要があります: "NET STOP W3SVC" と "NET START W3SVC"。  
  
4.  RegEdit ユーティリティを使用して、レジストリ内を "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" に移動し、 **RDSServer**という名前のキーがあることを確認します。 そうでない場合は、作成します。  
  
5.  インターネットサービスマネージャーを使用して、既定の Web サイトに移動し、MSADC 仮想ルートのプロパティを表示します。 ディレクトリのセキュリティ/IP アドレスとドメイン名の制限を調べます。 [アクセスが拒否されました] がオンになっている場合は、[許可] を選択します。  
  
 最初に問題の解決についての変更が表示されない場合は、サーバーの再起動を試してください。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントは Windows オペレーティングシステムに含まれなくなりました。 RDS を使用するアプリケーションを [WCF Data Service](/dotnet/framework/wcf/)に移行します。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)