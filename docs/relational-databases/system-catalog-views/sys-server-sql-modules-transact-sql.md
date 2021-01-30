---
description: sys.server_sql_modules (Transact-sql)
title: sys.server_sql_modules (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4113ba2be9e77d964d9b9bbfa9ae35f71e6adf8f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99172607"
---
# <a name="sysserver_sql_modules-transact-sql"></a>sys.server_sql_modules (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  TR 型のサーバーレベルのトリガーの SQL モジュールのセットを格納します。 このリレーションは sys.server_triggers に結合できます。 組 (object_id) はリレーションのキーです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|これは、このモジュールが定義されているサーバーレベルのトリガーへの外部キー参照です。|  
|**カスタム**|**nvarchar(max)**|このモジュールを定義する SQL テキスト。<br /><br /> NULL = 暗号化されています。|  
|**uses_ansi_nulls**|**bit**|モジュールは ANSI NULLS 設定オプションを ON に設定して作成されました。|  
|**uses_quoted_identifier**|**bit**|モジュールは、引用符で囲まれた識別子の set オプションが ON に設定されて作成されました。|  
|**execute_as_principal_id**|**int**|EXECUTE AS サーバー プリンシパルの ID。<br /><br /> 既定、または EXECUTE AS CALLER の場合は、NULL です。<br /><br /> 指定されたプリンシパルの ID。 EXECUTE AS SELF EXECUTE as principal-2 = EXECUTE AS OWNER です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
