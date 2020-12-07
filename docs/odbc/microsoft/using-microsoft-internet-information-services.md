---
description: Microsoft インターネット インフォメーション サービスの使用
title: Microsoft インターネットインフォメーションサービス | を使用するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e20a15aad4409f535d83e813fdfbd911ca80674
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471334"
---
# <a name="using-microsoft-internet-information-services"></a>Microsoft インターネット インフォメーション サービスの使用
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 IIS スクリプト内からの接続が困難な場合 (特に、ORA-12641 エラーが発生した場合)、次の行を Sqlnet. ORA ファイルに追加します。  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 これにより、セキュリティで保護された Network Services が無効になり、匿名認証を使用して接続できるようになります。
