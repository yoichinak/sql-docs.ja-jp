---
description: カスタマイズ ファイルの Connect セクション
title: カスタマイズファイルの接続セクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: rothja
ms.author: jroth
ms.openlocfilehash: c4350cb9aad6e2ef1d9381cffb6e05b13d09c43c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724783"
---
# <a name="customization-file-connect-section"></a>カスタマイズ ファイルの Connect セクション
ハンドラーの既定の動作では、すべての接続が拒否されます。 **Connect**セクションでは、その動作に対する例外を指定します。 たとえば、すべての **接続** セクションが存在しないか空の場合、既定では接続を確立できませんでした。  
  
 **Connect**セクションには次のものを含めることができます。  
  
-   この接続で許可される既定の読み取り操作と書き込み操作を指定する既定のアクセスエントリ。 セクションに既定のアクセスエントリがない場合、セクションは無視されます。  
  
-   クライアント接続文字列を置き換える新しい接続文字列。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
 既定のアクセスエントリの形式は次のとおりです。  
  
```console
  
Access=  
accessRight  
  
```  
  
 置換接続文字列のエントリの形式は次のとおりです。  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>解説  
  
|要素|説明|  
|----------|-----------------|  
|**接続する**|これが接続文字列エントリであることを示すリテラル文字列。|  
|**_connectionString_**|クライアント接続文字列全体を置き換える文字列。|  
|**Access (アクセス)**|これがアクセスエントリであることを示すリテラル文字列。|  
|**_accessRight_**|次のいずれかのアクセス権。<br /><br /> -   **NoAccess** -ユーザーはデータソースにアクセスできません。<br />-   **ReadOnly** -ユーザーはデータソースを読み取ることができます。<br />-   **ReadWrite** -ユーザーは、データソースに対して読み取りまたは書き込みを行うことができます。|  
  
 任意の接続を許可する (実質的に既定のハンドラー動作を無効にする) 場合は、[ **既定の接続** ] セクションのアクセスエントリをに設定 `Access=ReadWrite` し、他の [ **接続** _id_ ] セクションを削除またはコメントアウトします。  
  
## <a name="see-also"></a>参照  
 [カスタマイズファイルログセクション](./customization-file-logs-section.md)   
 [カスタマイズファイル SQL セクション](./customization-file-sql-section.md)   
 [カスタマイズファイルの UserList セクション](./customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](./datafactory-customization.md)   
 [必要なクライアント設定](./required-client-settings.md)   
 [カスタマイズファイルについて](./understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](./writing-your-own-customized-handler.md)