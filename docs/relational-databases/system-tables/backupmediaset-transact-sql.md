---
title: backupmediaset (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fded40f11cfc094e3af89295496787413e3fd4cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540380"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  バックアップ メディア セットごとに 1 行のデータを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|一意のメディアセット識別番号。 Id、主キー。|  
|**media_uuid**|**uniqueidentifier**|メディアセットの UUID。 すべて [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメディアセットに UUID があります。<br /><br /> 以前のバージョンのでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メディアセットに1つのメディアファミリしか含まれていない場合、 **media_uuid** 列が NULL になることがあります (**media_family_count** は 1)。|  
|**media_family_count**|**tinyint**|メディア セット内のメディア ファミリの数。 NULL にすることができます。|  
|**name**|**nvarchar(128)**|メディアセットの名前。 NULL にすることができます。<br /><br /> 詳細については、「 [バックアップ &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)」の「MEDIANAME と MEDIADESCRIPTION」を参照してください。|  
|**description**|**nvarchar (255)**|メディア セットの説明。 NULL にすることができます。<br /><br /> 詳細については、「 [バックアップ &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)」の「MEDIANAME と MEDIADESCRIPTION」を参照してください。|  
|**software_name**|**nvarchar(128)**|メディアラベルを書き込んだバックアップソフトウェアの名前。 NULL にすることができます。|  
|**software_vendor_id**|**int**|バックアップ メディア ラベルを記述したソフトウェア ベンダーの識別番号。 NULL にすることができます。<br /><br /> の値 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は16進数の0x1200 です。|  
|**MTF_major_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]このメディアセットの生成に使用されるテープ形式のメジャーバージョン番号。 NULL にすることができます。|  
|**mirror_count**|**tinyint**|メディアセット内のミラーの数。|  
|**is_password_protected**|**bit**|メディアセットパスワードが保護されているかを示します。<br /><br /> 0 = 保護されていない<br /><br /> 1 = 保護されている|  
|**is_compressed**|**bit**|バックアップが圧縮されているかどうか。<br /><br /> 0 = 圧縮されていません。<br /><br /> 1 = 圧縮<br /><br /> この値は、 **msdb** のアップグレード中に NULL に設定されます。 これは圧縮されていないバックアップを示します。|  
|**is_encrypted**|**ビット**|バックアップが暗号化されているかどうか。<br /><br /> 0 = 暗号化なし<br /><br /> 1 = 暗号化|  
  
## <a name="remarks"></a>解説  
 LOADHISTORY を使用した *backup_device* からの RESTORE verifyonly は、 **backupmediaset** テーブルの列に、メディアセットヘッダーからの適切な値を設定します。  
  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
