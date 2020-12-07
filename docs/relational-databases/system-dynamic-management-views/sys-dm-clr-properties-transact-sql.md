---
description: sys.dm_clr_properties (Transact-SQL)
title: dm_clr_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7f966cbb5570eb1efb2068d7796ccecb4463750
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551302"
---
# <a name="sysdm_clr_properties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の共通言語ランタイム (CLR) 統合に関係するプロパティごとに 1 行のデータを返します。このプロパティには、ホストされる CLR のバージョンや状態などが含まれます。 ホストされる CLR は、 [CREATE assembly](../../t-sql/statements/create-assembly-transact-sql.md)、 [ALTER assembly](../../t-sql/statements/alter-assembly-transact-sql.md)、または [DROP assembly](../../t-sql/statements/drop-assembly-transact-sql.md) ステートメントを実行するか、任意の CLR ルーチン、型、またはトリガーを実行することによって初期化されます。 **Dm_clr_properties**ビューでは、ユーザー clr コードの実行がサーバーで有効になっているかどうかは指定されません。 [Clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)オプションを1に設定して[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)ストアドプロシージャを使用すると、ユーザー clr コードの実行が有効になります。  
  
 **Dm_clr_properties**ビューには、[**名前**] 列と [**値**] 列があります。 このビューの各行には、ホストされている CLR のプロパティに関する詳細が表示されます。 このビューを使用して、ホストされる CLR に関する情報 (CLR のインストール ディレクトリ、CLR のバージョン、ホストされる CLR の現在の状態など) を収集します。 このビューは、サーバーコンピューターでの CLR のインストールに関する問題が原因で、CLR 統合コードが動作していないかどうかを判断するのに役立ちます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|プロパティの名前。|  
|**value**|**nvarchar(128)**|プロパティの値。|  
  
## <a name="properties"></a>Properties  
 **ディレクトリ**プロパティは、.NET Framework がサーバーにインストールされたディレクトリを示します。 サーバーコンピューターに複数の .NET Framework がインストールされている可能性があります。このプロパティの値によって、どのインストール [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用されているかが識別されます。  
  
 **Version**プロパティは、サーバー上の .NET Framework およびホストされている CLR のバージョンを示します。  
  
 **Dm_clr_properties**動的マネージビューは、**状態**プロパティに対して6つの異なる値を返すことができます。これには、ホストされる clr の状態が反映されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] これらは次のとおりです。  
  
-   Mscoree is not loaded. (mscoree が読み込まれていない。)  
  
-   Mscoree is loaded. (mscoree が読み込まれている。)  
  
-   Mscoree.dll を使用したロックされた CLR バージョン。  
  
-   CLR が初期化されています。  
  
-   CLR を完全に初期化できませんでした。  
  
-   CLR が停止しています。  
  
 **Mscoree.dll が読み込まれておらず**、 **mscoree.dll が読み込ま**れている状態は、サーバー起動時にホストされている CLR 初期化の進行状況を示していますが、表示されない可能性があります。  
  
 **Mscoree.dll 状態のロック**された clr バージョンは、ホストされている clr が使用されていないため、まだ初期化されていない場合に表示されることがあります。 ホストされる CLR は、DDL ステートメント ( [CREATE ASSEMBLY &#40;transact-sql&#41;](../../t-sql/statements/create-assembly-transact-sql.md)など) またはマネージデータベースオブジェクトが実行されるときに初期化されます。  
  
 **Clr が初期化**された状態は、ホストされている clr が正常に初期化されたことを示します。 これは、ユーザー CLR コードの実行が有効になっているかどうかを示すものではないことに注意してください。 ユーザー CLR コードの実行が最初に有効になっていて、sp_configure ストアドプロシージャを使用して無効にした場合 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)でも、状態値は**CLR に初期化**されます。  
  
 **Clr 初期化が完全に失敗**した状態は、ホストされた clr の初期化が失敗したことを示します。 これは多くの場合メモリ不足が原因ですが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と CLR の間でホスティングのハンドシェイクが失敗していることも考えられます。 このような場合は、エラーメッセージ6512または6513がスローされます。  
  
 **CLR が停止状態**は、がシャットダウン処理中の場合にのみ表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 統合機能の強化により、このビューのプロパティおよび値は、の将来のバージョンで変更される可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
  
で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="examples"></a>例  
 次の例では、ホストされる CLR に関する情報を取得します。  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;共通言語ランタイム関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
