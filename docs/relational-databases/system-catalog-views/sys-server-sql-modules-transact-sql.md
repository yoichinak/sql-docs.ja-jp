---
description: server_sql_modules (Transact-sql)
title: server_sql_modules (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7f74b41384c2aa42c26623fa69ef35c74f49eab3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539583"
---
# <a name="sysserver_sql_modules-transact-sql"></a>server_sql_modules (Transact-sql)
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
  
  
