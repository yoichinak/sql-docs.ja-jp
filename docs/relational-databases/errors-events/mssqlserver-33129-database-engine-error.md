---
description: MSSQLSERVER_33129
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16340b6800ded7be2642f70496a09a16eb360274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456225"
---
# <a name="mssqlserver_33129"></a>MSSQLSERVER_33129
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|33129|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_CANNOT_DISABLE_WIN_GROUP|  
|メッセージ テキスト|ALTER_LOGIN を DISABLE 引数と共に使用して Windows グループへのアクセスを拒否することはできません。|  
  
## <a name="explanation"></a>説明  
このメッセージは、Windows グループのログインを無効にしようとしたときに発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
Windows グループのログインを無効にすることはできません。 Windows グループに許可されているアクセス権限を一時的に削除するには、Windows グループのログインの CONNECT 権限を REVOKE (取り消し) します。 この場合、Windows ユーザーは個人のログインまたは別の Windows グループを介してアクセスできる可能性があります。 次の例では、WESTCOAST ドメインの Accounting グループに対する CONNECT 権限を取り消します。  
  
```Transact-SQL  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
