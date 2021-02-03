---
description: MSSQL_ENG014144
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 892f71b9fbfafd6226b32e2f23d8bb85a4d9fe38
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198802"
---
# <a name="mssql_eng014144"></a>MSSQL_ENG014144
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|属性|値|  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14144|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|サブスクライバー '%s' を削除できません。 そのサブスクライバーのサブスクリプションがパブリケーション データベース '%s' にあります。|  
  
## <a name="explanation"></a>説明  
 サブスクライバーとして構成されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、そのインスタンスに対して構成されているアクティブなサブスクリプションがあると、サブスクライバーの役割から削除できません。  
  
## <a name="user-action"></a>ユーザーの操作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのサブスクライバーの状態を変更する前に、関連付けられているすべてのサブスクリプションを削除します。  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) を実行して、サブスクリプションを検索します。  
  
2.  パブリケーション データベースで [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) を実行して、サブスクリプションを削除します。  

## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
