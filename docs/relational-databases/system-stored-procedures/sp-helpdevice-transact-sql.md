---
description: sp_helpdevice (Transact-SQL)
title: sp_helpdevice (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 95c63d822851d7d1ccf9493e3e0d4cc9beedd624
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204742"
---
# <a name="sp_helpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Microsoft&#xAE; SQL Server&#x2122; のバックアップ デバイスに関する情報をレポートします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) カタログビューを使用することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @devname = ] 'name'` 情報を報告するバックアップデバイスの名前を指定します。 *Name* の値は常に **sysname** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|論理デバイス名。|  
|**physical_name**|**nvarchar(260)**|物理ファイル名。|  
|**description**|**nvarchar (255)**|デバイスの説明|  
|**status**|**int**|[ **説明** 列の状態の説明に対応する数値。|  
|**cntrltype**|**smallint**|デバイスのコントローラーの種類<br /><br /> 2 = ディスク デバイス<br /><br /> 5 = テープデバイス|  
|**size**|**int**|デバイスサイズ (2 KB ページ単位)。|  
  
## <a name="remarks"></a>コメント  
 *名前* を指定した場合、 **sp_helpdevice** 指定したダンプデバイスに関する情報が表示されます。 *名前* が指定されていない場合、 **sp_helpdevice** は **sys.backup_devices** カタログビューのすべてのダンプデバイスに関する情報を表示します。  
  
 ダンプデバイスは **sp_addumpdevice** を使用してシステムに追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、のインスタンス上のすべてのダンプデバイスに関する情報をレポート [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>参照  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
