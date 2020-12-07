---
description: カスタマイズ ファイルの UserList セクション
title: カスタマイズファイル UserList Section |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: rothja
ms.author: jroth
ms.openlocfilehash: b09e5f9356ad196e03c970623369d4918a6f5506
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724753"
---
# <a name="customization-file-userlist-section"></a>カスタマイズ ファイルの UserList セクション
**Userlist**セクションは、同じセクション*識別子*パラメーターを持つ**connect**セクションに関連しています。  
  
 このセクションには、指定されたユーザーのアクセス権を指定する*ユーザーアクセスエントリ*を含めることができます。また、[一致する**接続**] セクションの*既定*の*アクセスエントリ*を上書きします。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
 ユーザーアクセスエントリの形式は次のとおりです。  
  
 _ユーザー名_**=**   
 **_accessRights_**  
  
|要素|説明|  
|----------|-----------------|  
|*userName*|この接続を採用している *ユーザーのユーザー名* 。 有効なユーザー名は、[IIS **Service Manager** ] ダイアログで確立されます。|  
|**_accessRights_**|次のいずれかのアクセス権。<br /><br /> -   **NoAccess** -ユーザーはデータソースにアクセスできません。<br />-   **ReadOnly** -ユーザーはデータソースを読み取ることができます。<br />-   **ReadWrite** -ユーザーは、データソースに対して読み取りまたは書き込みを行うことができます。|  
  
## <a name="see-also"></a>参照  
 [カスタマイズファイルの接続セクション](./customization-file-connect-section.md)   
 [カスタマイズファイルログセクション](./customization-file-logs-section.md)   
 [カスタマイズファイル SQL セクション](./customization-file-sql-section.md)   
 [DataFactory のカスタマイズ](./datafactory-customization.md)   
 [必要なクライアント設定](./required-client-settings.md)   
 [カスタマイズファイルについて](./understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](./writing-your-own-customized-handler.md)