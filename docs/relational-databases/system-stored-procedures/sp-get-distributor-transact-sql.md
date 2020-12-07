---
description: sp_get_distributor (Transact-SQL)
title: sp_get_distributor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6cdc15f66c918b0d320c9c2ad2106fbded5fc256
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549745"
---
# <a name="sp_get_distributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ディストリビューターがサーバーにインストールされているかどうかを調べます。 このストアド プロシージャは、任意のデータベース上の、ディストリビューターを検索しているコンピューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ら**|**int**|**0** = いいえ、 **1** = はい|  
|**ディストリビューションサーバー**|**sysname**|ディストリビューター サーバーの名前。|  
|**インストールされているディストリビューション db**|**int**|**0** = いいえ、 **1** = はい|  
|**is distribution publisher**|**int**|**0** = いいえ、 **1** = はい|  
|**リモートディストリビューションパブリッシャーがある**|**int**|**0** = いいえ、 **1** = はい|  
  
## <a name="remarks"></a>解説  
 **sp_get_distributor** は、主に、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーが **sp_get_distributor**を実行できます。 ディストリビューションデータベースの固定データベースロール **db_owner** または **replmonitor** のメンバー、または少なくとも1つのパブリッシュされたデータベースの **db_owner** 固定データベースロールのメンバーによって、このストアドプロシージャが実行されると、NULL 以外の結果セットが返されます。 また、少なくとも1つのパブリッシュされたデータベースのパブリケーションアクセスリスト (PAL) のユーザーがこのストアドプロシージャを実行した場合、または SQL Server 以外のパブリッシャーのディストリビューションデータベースの PAL で **sp_get_distributor**も、NULL 以外の結果セットが返されます。  
  
## <a name="see-also"></a>参照  
 [パブリッシングとディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [ディストリビューターおよびパブリッシャーの情報スクリプト](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
