---
description: MSsubscriber_info (Transact-sql)
title: MSsubscriber_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d949fe0234cad850a1080b727f0917df6e6a24af
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89523879"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscriber_info**テーブルには、ローカルディストリビューターからプッシュされたサブスクリプションのパブリッシャー/サブスクライバーのペアごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
 **メモ** このシステムテーブルは非推奨とされており、以前のバージョンのをサポートするために保持されてい [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前です。|  
|**type**|**tinyint**|サブスクライバーの種類:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバー。<br /><br /> **1** = ODBC データソース。|  
|**ログイン**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログインです。 サブスクライバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードで追加されている場合は、暗号化形式で格納されます。|  
|**password**|**nvarchar (524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のパスワードです。 サブスクライバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードで追加されている場合は、暗号化形式で格納されます。|  
|**description**|**nvarchar (255)**|サブスクライバーの説明。|  
|**security_mode**|**int**|実装されているセキュリティ モードです。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
