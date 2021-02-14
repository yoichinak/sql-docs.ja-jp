---
description: sys.sp_add_trusted_assembly (Transact-SQL)
title: sys.sp_add_trusted_assembly (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e978bdf7dacc6c00dd1861ea3f54f7b1699c6665
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100076008"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys.sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

サーバーの信頼されたアセンブリの一覧にアセンブリを追加します。

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>構文
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>解説  

この手順では、  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)にアセンブリを追加します。

## <a name="arguments"></a>引数

[ @hash =] '*値*'  
サーバーの信頼されたアセンブリの一覧に追加するアセンブリの SHA2_512 ハッシュ値。 アセンブリが署名されていないか、データベースが信頼できるものとしてマークされていない場合でも、 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md) が有効になっていると、信頼されたアセンブリが読み込まれる

[ @description =] '*description*'  
アセンブリに関するオプションのユーザー定義の説明。 信頼するアセンブリの簡易名、バージョン番号、カルチャ、公開キー、およびアーキテクチャをエンコードする正規名を使用することをお勧めします。 この値は、共通言語ランタイム (CLR) 側でアセンブリを一意に識別するものであり、sys. アセンブリの clr_name 値と同じです。 

## <a name="permissions"></a>アクセス許可

`sysadmin`固定サーバーロールまたは権限のメンバーシップが必要 `CONTROL SERVER` です。

## <a name="examples"></a>例  

次の例では、という名前のアセンブリ `pointudt` をサーバーの信頼されたアセンブリの一覧に追加します。 これらの値は、  [sys. アセンブリ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)から入手できます。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>参照  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

