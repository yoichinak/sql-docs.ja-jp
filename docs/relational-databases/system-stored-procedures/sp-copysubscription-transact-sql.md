---
description: sp_copysubscription (Transact-sql)
title: sp_copysubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e4a80092356c6508c7ef1f8408d5573c8014fdc0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89528105"
---
# <a name="sp_copysubscription-transact-sql"></a>sp_copysubscription (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

    
> [!IMPORTANT]  
>  アタッチ可能なサブスクリプション機能は非推奨とされており、今後のリリースでは削除される予定です。 新しい開発作業では、この機能を使用しないでください。 パラメーター化されたフィルターを使用してパーティション分割されたマージ パブリケーションでは、パーティション スナップショットの新しい機能を使用することをお勧めします。この機能を使用すると、多数のサブスクリプションの初期化を簡単に実行できます。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。 パーティション分割されていないパブリケーションの場合は、バックアップを使用してサブスクリプションを初期化できます。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
 プル サブスクリプションはあるがプッシュ サブスクリプションはないサブスクリプション データベースをコピーします。 単一ファイルのデータベースのみをコピーできます。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>引数  
`[ @filename = ] 'file_name'` データファイル (.mdf) のコピーの保存先となる完全なパス (ファイル名を含む) を指定する文字列を指定します。 *ファイル名* は **nvarchar (260)**,、既定値はありません。  
  
`[ @temp_dir = ] 'temp_dir'` 一時ファイルが格納されているディレクトリの名前を指定します。 *temp_dir* は **nvarchar (260)**,、既定値は NULL です。 NULL の場合、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既定のデータディレクトリが使用されます。 このディレクトリは、すべてのサブスクライバー データベース ファイルを合わせたファイル サイズを格納できるだけの領域を備えている必要があります。  
  
`[ @overwrite_existing_file = ] 'overwrite_existing_file'`** \@ Filename**に指定されているものと同じ名前の既存のファイルを上書きするかどうかを指定する、省略可能なブール型のフラグです。 *overwrite_existing_file*は **ビット**,、既定値は **0**です。 **1**の場合、 ** \@ filename**によって指定されたファイルを上書きします (存在する場合)。 **0**の場合、ファイルが存在する場合、ストアドプロシージャは失敗し、ファイルは上書きされません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_copysubscription** は、サブスクライバーでスナップショットを適用する代わりに、サブスクリプションデータベースをファイルにコピーするために、すべての種類のレプリケーションで使用されます。 プルサブスクリプションのみをサポートするようにデータベースを構成する必要があります。 適切な権限を持つユーザーは、サブスクリプションデータベースのコピーを作成し、サブスクリプションファイル (msf) を別のサブスクライバーに電子メール、コピー、または転送することができます。その後、サブスクリプションとしてアタッチできます。  
  
 コピーするサブスクリプションデータベースのサイズは 2 gb 未満である必要があります。  
  
 **sp_copysubscription** は、クライアントサブスクリプションを持つデータベースでのみサポートされており、データベースにサーバーサブスクリプションがある場合は実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_copysubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [代替スナップショットフォルダーの場所](../../relational-databases/replication/snapshot-options.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
