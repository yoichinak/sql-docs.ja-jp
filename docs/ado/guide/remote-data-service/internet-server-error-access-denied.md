---
description: 'インターネット サーバー エラー: アクセス拒否'
title: 'インターネットサーバーエラー: アクセスが拒否されました |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cf9b2010fdbb20522c774d4c54ce2773cf817c5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721563"
---
# <a name="internet-server-error-access-denied"></a>インターネット サーバー エラー: アクセス拒否
このエラーが発生した場合は、通常、Microsoft インターネットインフォメーションサービス (IIS) が次の状態を返したことを意味します。  
  
 HTTP_STATUS_DENIED 401  
  
 IIS によってアクセスされるディレクトリに適切なアクセス許可があることを確認します。 RDS は、匿名、基本、または NT チャレンジ/応答 (Windows 2000 では統合 Windows 認証と呼ばれます) の3つのパスワード認証モードのいずれかで実行されている IIS Web サーバーと通信できます。 また、Web サーバーが Windows NT/Windows 2000 コンピューターの場合は、データソースコンピューターに対するアクセス許可が必要です。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)