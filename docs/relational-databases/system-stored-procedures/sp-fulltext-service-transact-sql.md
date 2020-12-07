---
description: sp_fulltext_service (Transact-SQL)
title: sp_fulltext_service (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f29ad11ca5b1df94e445466a5402637a2abab023
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546122"
---
# <a name="sp_fulltext_service-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索のサーバー プロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>引数  
`[ @action = ] 'action'` 変更またはリセットするプロパティを指定します。 *アクション* は **nvarchar (100),、** 既定値はありません。 *C*プロパティとその説明、および設定できる値の一覧については、「 *value*引数」の表を参照してください。 この引数によって返されるプロパティには、データ型、現在の実行値、最小値または最大値、非推奨のステータスなどがあります。  
  
`[ @value = ] value` 指定されたプロパティの値です。 *値* は **sql_variant**,、既定値は NULL です。 @valueが null の場合 **、sp_fulltext_service**は現在の設定を返します。 次の表は、アクション プロパティとその説明、および設定できる値の一覧です。  
  
> [!NOTE]  
>  次の操作は、の将来のリリースで削除される予定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です: **clean_up**、 **connect_timeout**、 **data_timeout**、および **resource_usage**。 新しい開発作業ではこれらのアクションの使用を避け、現在これらのアクションを使用しているアプリケーションの変更を検討してください。  
  
|アクション|データ型|説明|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に0です。|  
|**connect_timeout**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に0です。|  
|**data_timeout**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に0です。|  
|**load_os_resources**|**int**|オペレーティング システムのワード ブレーカー、ステミング機能、およびフィルターを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録し、使用するかどうかを指定します。 つぎのいずれかです。<br /><br /> 0 = この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス固有のフィルターとワード ブレーカーのみを使用<br /><br /> 1 = オペレーティング システムのフィルターとワード ブレーカーを読み込む<br /><br /> オペレーティング システムに行われた更新によって予期しない動作が起こるのを防ぐため、既定ではこのプロパティは無効になっています。 オペレーティングシステムリソースの使用を有効にすると、インスタンス固有のリソースがインストールされていないインデックスサービスに登録されている言語とドキュメントの種類のリソースにアクセスできるように [!INCLUDE[msCoName](../../includes/msconame-md.md)] なります。 オペレーティングシステムリソースの読み込みを有効にした場合は、オペレーティングシステムのリソースが信頼された署名付きバイナリであることを確認します。それ以外の場合は、 **verify_signature** (下記参照) が1に設定されていると、読み込むことができません。|  
|**master_merge_dop**|**int**|マスターマージプロセスによって使用されるスレッドの数を指定します。 この値は、使用可能な Cpu または CPU コアの数を超えることはできません。<br /><br /> この引数が指定されていない場合、サービスは4のうちの小さい方、または使用可能な cpu または CPU コアの数を使用します。|  
|**pause_indexing**|**int**|現在一時停止されている場合は、フルテキストインデックス作成を一時停止するか、現在実行中であるか再開するかを指定します。<br /><br /> 0 = サーバー インスタンスのフルテキスト インデックス作成を再開する<br /><br /> 1 = サーバーインスタンスのフルテキストインデックス作成操作を一時停止します。|  
|**resource_usage**|**int**|以降のバージョンには関数がない [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ため、は無視されます。|  
|**update_languages**|NULL|フルテキスト検索に登録された言語の一覧を更新します。 これらの言語は、インデックス作成とフルテキストクエリの構成時に指定します。 フィルターデーモンホストは、 **varbinary**、 **varbinary (max)**、 **image**、 **xml**など、フルテキストインデックス作成のために、データ型に格納されている .docx など、対応するファイル形式からテキスト情報を抽出するためにフィルターを使用します。<br /><br /> 詳細については、「 [登録済みのフィルターおよびワード ブレーカーの表示または変更](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)」を参照してください。|  
|**upgrade_option**|**int**|データベースを [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] からそれより新しいバージョンにアップグレードする際のフルテキスト インデックスの移行方法を制御します。 このプロパティは、データベースのインポート、データベース バックアップの復元、ファイル バックアップの復元、またはデータベース コピー ウィザードを使用したデータベースのコピーによってアップグレードする場合に適用されます。<br /><br /> つぎのいずれかです。<br /><br /> 0 = フルテキストカタログは、新しい拡張されたワードブレーカーを使用して再構築されます。 インデックスの再構築には時間がかかり、アップグレード後にかなりの量の CPU とメモリが必要になる可能性があります。<br /><br /> 1 = フルテキスト カタログがリセットされます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のフルテキスト カタログ ファイルは削除されますが、フルテキスト カタログのメタデータおよびフルテキスト インデックスは保持されます。 アップグレード後、すべてのフルテキスト インデックスで変更の追跡は無効化されており、クロールは自動的には開始されません。 アップグレードの完了後、手動で完全作成を実行するまで、カタログは空のままになります。<br /><br /> 2 = フルテキストカタログがインポートされます。 通常、インポートの方が再構築よりもかなり高速に処理されます。 たとえば、CPU を 1 つだけ使用している場合、インポートは、再構築の約 10 倍の速さで実行されます。 ただし、インポートされたフルテキストカタログは、新しい拡張されたワードブレーカーを使用しないため、最終的にフルテキストカタログを再構築することが必要になる場合があります。<br /><br /> 注: 再構築はマルチスレッドモードで実行できます。また、10個を超える Cpu が使用可能な場合は、再構築によってすべての Cpu を使用できるようになると、インポートよりも再構築が高速に実行される可能性があります。<br /><br /> フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 このオプションは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースでのみ使用できます。<br /><br /> フルテキスト アップグレード オプションの選択については、「[フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」をご覧ください。<br /><br /> 注: でこのプロパティを設定するに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、" **フルテキストアップグレードオプション** " プロパティを使用します。 詳細については、「 [サーバー インスタンスでのフルテキスト検索の管理と監視](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)」を参照してください。|  
|**verify_signature**|**int**|フルテキストエンジンによって署名付きバイナリのみが読み込まれるかどうかを示します。 既定では、信頼された署名付きバイナリのみが読み込まれます。<br /><br /> 1 = 信頼された署名付きバイナリのみを確認して読み込む (既定値)<br /><br /> 0 = バイナリが署名付きかどうかを確認しない|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_fulltext_service**を実行できるのは、 **serveradmin**固定サーバーロールのメンバー、またはシステム管理者だけです。  
  
## <a name="examples"></a>例  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. 登録されている言語の一覧を更新する  
 次の例では、フルテキスト検索に登録された言語の一覧を更新します。  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. フルテキスト カタログをリセットするようにフルテキスト アップグレード オプションを変更する  
 次の例では、フルテキストカタログをリセットするようにフルテキストアップグレードオプションを変更します。 これにより、それらが完全に削除されます。 この例では、省略可能な `@action` キーワードとキーワードを指定し `@value` ます。  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
