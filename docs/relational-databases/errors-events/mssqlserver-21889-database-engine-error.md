---
description: MSSQLSERVER_21889
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: df5581450e8c1901187b9e96d37590008c4e75b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88332288"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|21889|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21889|  
|メッセージ テキスト|SQL サーバー インスタンス '%s' はレプリケーション パブリッシャーではありません。 このインスタンスがパブリッシング データベース '%s' をホストできるようにするために、SQL Server インスタンス '%s' で、ディストリビューター '%s' を指定して **sp_adddistributor** を実行します。 元のパブリッシャーで使用されているものと同じログインおよびパスワードを指定していることを確認してください。|  
  
## <a name="explanation"></a>説明  
パブリッシャー データベースをホストするためには、SQL Server のインスタンスがレプリケーション パブリッシャーである必要があります。 **sp_validate_redirected_publisher** は、リモート サーバーで **sp_helpdistributor** を呼び出し、サーバーがレプリケーション パブリッシャーであるかどうかを判断します。 このエラーは、SQL Server のターゲット インスタンスがレプリケーション パブリッシャーではないことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
パブリッシャー データベースをホストする SQL Server のインスタンスで **sp_adddistributor** を実行します。 **sp_adddistributor** を実行するときに、正しいディストリビューターを指定します。 *\@password* パラメーターには、ディストリビューターで **sp_adddistributor** を最初に実行したときに使用したものと同じ値を使用します。  
  
