---
description: sp_addumpdevice (Transact-SQL)
title: sp_addumpdevice (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addumpdevice_TSQL
- sp_addumpdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], defining
- sp_addumpdevice
ms.assetid: c2d2ae49-0808-46d8-8444-db69a69d0ec3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1f17681ffbb922b25cffc6b21ecf2f6317d400db
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753794"
---
# <a name="sp_addumpdevice-transact-sql"></a>sp_addumpdevice (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から[現在のバージョン](../../sql-server/what-s-new-in-sql-server-2016.md)まで)。  

バックアップ デバイスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに追加します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addumpdevice [ @devtype = ] 'device_type'   
    , [ @logicalname = ] 'logical_name'   
    , [ @physicalname = ] 'physical_name'  
      [ , { [ @cntrltype = ] controller_type |  
          [ @devstatus = ] 'device_status' }  
      ]  
```  
  
## <a name="arguments"></a>引数  
`[ @devtype = ] 'device_type'` バックアップデバイスの種類を示します。 *device_type* は **varchar (20)** で、既定値はありません。次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**ディスク**|バックアップデバイスとしてのハードディスクファイル。|  
|**テープ**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows でサポートされるテープ デバイス。<br /><br /> 注:テープ バックアップ デバイスは、将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされなくなる予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。|  
  
`[ @logicalname = ] 'logical_name'` BACKUP ステートメントおよび RESTORE ステートメントで使用するバックアップデバイスの論理名を指定します。 *logical_name* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
`[ @physicalname = ] 'physical_name'` バックアップデバイスの物理名を指定します。 物理名は、オペレーティングシステムのファイル名の規則またはネットワークデバイスの汎用名前付け規則に従う必要があり、完全なパスを含める必要があります。 *physical_name* は **nvarchar (260)** で、既定値はありません。 NULL にすることはできません。  
  
 リモートネットワークの場所にバックアップデバイスを作成する場合は、を起動したときに使用されていた名前に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] リモートコンピューターに対する適切な書き込み機能があることを確認してください。  
  
 テープデバイスを追加する場合、このパラメーターには、Windows によってローカルテープデバイスに割り当てられた物理名を指定する必要があります。たとえば、コンピューター上の最初のテープデバイスの** \\ \\ .\TAPE0**です。 テープデバイスがサーバーコンピューターに接続されている必要があります。リモートで使用することはできません。 英数字以外の文字を含む名前は引用符で囲みます。  
  
> [!NOTE]  
>  このプロシージャは、指定された物理名をカタログに入力します。 この手順では、デバイスにアクセスしたり、デバイスを作成したりすることはありません。  
  
`[ @cntrltype = ] 'controller_type'` 公表. 指定した場合、このパラメーターは無視されます。 旧バージョンとの互換性のためだけに用意されています。 **Sp_addumpdevice**の新しい使用では、このパラメーターを省略する必要があります。  
  
`[ @devstatus = ] 'device_status'` 公表. 指定した場合、このパラメーターは無視されます。 旧バージョンとの互換性のためだけに用意されています。 **Sp_addumpdevice**の新しい使用では、このパラメーターを省略する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_addumpdevice** 、 **sys.backup_devices** カタログビューにバックアップデバイスを追加します。 その後、そのデバイスを BACKUP ステートメントや RESTORE ステートメントで論理的に参照できるようになります。 **sp_addumpdevice** では、物理デバイスへのアクセスは一切実行されません。 BACKUP ステートメントや RESTORE ステートメントが実行されるときにだけ、指定されたデバイスにアクセスされます。 論理バックアップデバイスを作成すると、BACKUP ステートメントと RESTORE ステートメントが簡略化されます。デバイス名を指定する場合は、"TAPE =" または "DISK =" 句を使用してデバイスパスを指定します。  
  
 所有権とアクセス許可の問題によって、ディスクまたはファイルバックアップデバイスの使用が妨げられることがあります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]を起動する Windows アカウントに適切なファイル権限が付与されているかどうかを確認してください。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、Windows でサポートされているテープ デバイスへのバックアップがサポートされます。 Windows でサポートされるテープ デバイスの詳細については、Windows のハードウェア互換性リストを参照してください。 コンピューターで使用できるテープ デバイスを表示するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用します。  
  
 ドライブの製造元によって提案された特定のテープドライブに対して、推奨されるテープのみを使用します。 DAT (digital audio tape) ドライブを使用している場合は、コンピューター用の DAT テープ (Digital Data Storage-DDS) を使用してください。  
  
 **sp_addumpdevice** をトランザクション内で実行することはできません。  
  
 デバイスを削除するには、 [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) または[SQL Server Management Studio](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **diskadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
 ディスクに対する書き込み権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-adding-a-disk-dump-device"></a>A. ディスクダンプデバイスを追加する  
 次の例では、という名前のディスクバックアップデバイスを `mydiskdump` 物理名で追加し `c:\dump\dump1.bak` ます。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak';  
```  
  
### <a name="b-adding-a-network-disk-backup-device"></a>B. ネットワークディスクバックアップデバイスを追加する  
 次の例では、`networkdevice` というリモートのディスク バックアップ デバイスを追加します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]を起動する名前には、そのリモート ファイル (`\\<servername>\<sharename>\<path>\<filename>.bak`) を扱う権限が必要です。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'networkdevice',  
    '\\<servername>\<sharename>\<path>\<filename>.bak';  
```  
  
### <a name="c-adding-a-tape-backup-device"></a>C. テープ バックアップ デバイスを追加する  
 次の例では、 `tapedump1` 物理名を使用してデバイスを追加し `\\.\tape0` ます。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0';  
```  
  
### <a name="d-backing-up-to-a-logical-backup-device"></a>D. 論理バックアップデバイスへのバックアップ  
 次の例では、 `AdvWorksData` バックアップディスクファイル用の論理バックアップデバイスを作成します。 作成した論理バックアップ デバイスに [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースをバックアップします。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\AdvWorksData.bak';  
GO  
BACKUP DATABASE AdventureWorks2012   
 TO AdvWorksData  
   WITH FORMAT;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
