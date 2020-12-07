---
description: sp_scriptdynamicupdproc (Transact-sql)
title: sp_scriptdynamicupdproc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords:
- sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 03be0aa206a4037de5e09e202e38fcce5ecf5a6c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525950"
---
# <a name="sp_scriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  動的な更新ストアド プロシージャを作成する CREATE PROCEDURE ステートメントを生成します。 カスタムストアドプロシージャ内の UPDATE ステートメントは、変更する列を示す MCALL 構文に基づいて動的に作成されます。 このストアドプロシージャは、サブスクライブしているテーブルのインデックスの数が増加しており、変更される列の数が少ない場合に使用します。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>引数  
`[ @artid = ] artid` アーティクル ID を示します。 *artid* は **int**,、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
 1つの **nvarchar (4000)** 列で構成される結果セットを返します。 結果セットは、カスタムストアドプロシージャの作成に使用される CREATE PROCEDURE ステートメント全体を形成します。  
  
## <a name="remarks"></a>解説  
 **sp_scriptdynamicupdproc** は、トランザクションレプリケーションで使用します。 既定の MCALL スクリプト作成ロジックでは、UPDATE ステートメント内のすべての列を対象に、ビットマップを使用して、変更された列が特定されます。 列が変更されていない場合は、列がそれ自体に戻されます。この場合、通常は問題は発生しません。 列にインデックスが作成されている場合、追加の処理が発生します。 動的なアプローチには、変更された列のみが含まれます。これにより、最適な更新文字列が提供されます。 ただし、動的更新ステートメントがビルドされると、実行時に余分な処理が発生します。 動的な方法と静的な方法の両方をテストし、最適な方を選択することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_scriptdynamicupdproc**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、 **pubs**データベースの**authors**テーブルで ( *artid*が**1**に設定された) アーティクルを作成し、UPDATE ステートメントが実行するカスタムプロシージャであることを指定します。  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 パブリッシャーで次のストアドプロシージャを実行して、サブスクライバーでディストリビューションエージェントによって実行されるカスタムストアドプロシージャを生成します。  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 このストアド プロシージャを実行した後、結果のスクリプトを使用して、サブスクライバー側で手動でストアド プロシージャを作成できます。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
