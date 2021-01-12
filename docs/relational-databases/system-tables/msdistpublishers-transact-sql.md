---
description: MSdistpublishers (Transact-sql)
title: MSdistpublishers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: cawrites
ms.author: chadam
ms.openlocfilehash: 296bedcc14194dbba3a8f91cb8ebbc6553b6481c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098209"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Msdistpublishers** テーブルには、ローカルディストリビューターによってサポートされるリモートパブリッシャーごとに1つの行が含まれます。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|パブリッシャーディストリビューターの名前。|  
|**distribution_db**|**sysname**|ディストリビューションデータベースの名前。|  
|**working_directory**|**nvarchar (255)**|パブリケーションのデータとスキーマファイルを格納するために使用する作業ディレクトリの名前。|  
|**security_mode**|**int**|ディストリビューターで実装されているセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。<br /><br /> **1** = Windows 認証。|  
|**ログイン**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログイン ID です。|  
|**password**|**nvarchar (524)**|認証用のパスワード (暗号化されたもの) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**active**|**bit**|ローカルディストリビューターがリモートパブリッシャーによって使用されているかどうかを示します。|  
|**テッド**|**bit**|リモートパブリッシャーがローカルディストリビューターと同じパスワードを使用するかどうかを示します。<br /><br /> **0** = ディストリビューターに接続するために、リモートパブリッシャーでパスワードが必要です。<br /><br /> **1** = パスワードは必要ありません。|  
|**third_party**|**bit**|パブリッシャーがインストールされているかどうかを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール。**1** = 異種データソース。|  
|**publisher_type**|**sysname**|パブリッシャーの種類:<br /><br />   =  MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]文書.<br /><br /> **Oracle** = Standard oracle パブリッシャー。<br /><br /> **ORACLE gateway** = Oracle ゲートウェイパブリッシャー。|  
|**storage_connection_string**|**nvarchar (779)**|Azure SQL Database ストレージ接続文字列の値。|  

  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
