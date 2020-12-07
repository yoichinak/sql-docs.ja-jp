---
description: sys.syscacheobjects (Transact-SQL)
title: sys.syscacheobjects (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscacheobjects_TSQL
- sys.syscacheobjects
- syscacheobjects
- syscacheobjects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscacheobjects system table
- sys.syscacheobjects compatibility view
ms.assetid: 9b14f37c-b7f5-4f71-b070-cce89a83f69e
author: rothja
ms.author: jroth
ms.openlocfilehash: 25160eb8e7a25e2a4ec6d2f8b318fc78e7af61ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88399678"
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  キャッシュの使用方法に関する情報が含まれています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**bucketid**|**int**|バケット ID です。 値は 0 ～ディレクトリ サイズ -1 の範囲を示します。 ディレクトリサイズは、ハッシュテーブルのサイズです。|  
|**cacheobjtype**|**nvarchar(17)**|キャッシュ内のオブジェクトの種類です。<br /><br /> コンパイル済みプラン<br /><br /> 実行プラン<br /><br /> 解析ツリー<br /><br /> カーソル<br /><br /> 拡張ストアド プロシージャ|  
|**objtype**|**nvarchar(8)**|オブジェクトの種類:<br /><br /> ストアド プロシージャ<br /><br /> 準備済みステートメント<br /><br /> アドホッククエリ ( [!INCLUDE[tsql](../../includes/tsql-md.md)] リモートプロシージャコールではなく、 **sqlcmd** ユーティリティまたは **osql** ユーティリティから言語イベントとして送信されます)<br /><br /> ReplProc (レプリケーションプロシージャ)<br /><br /> トリガー<br /><br /> View<br /><br /> Default<br /><br /> ユーザー テーブル<br /><br /> システム テーブル<br /><br /> ○<br /><br /> ルール|  
|**objid**|**int**|キャッシュ内のオブジェクトを検索するために使用される主キーの1つ。 これは、データベースオブジェクト (プロシージャ、ビュー、トリガーなど) の **sysobjects** に格納されているオブジェクト ID です。 アドホックまたは準備された SQL などのキャッシュオブジェクトの場合、 **objid** は内部で生成された値です。|  
|**dbid**|**smallint**|キャッシュオブジェクトがコンパイルされたデータベース ID。|  
|**dbidexec**|**smallint**|クエリ実行元となるデータベース ID です。<br /><br /> ほとんどのオブジェクトでは、 **dbidexec** の値は **dbid**と同じです。<br /><br /> システムビューの場合、 **dbidexec** は、クエリの実行元のデータベース ID です。<br /><br /> アドホッククエリの場合、 **dbidexec** は0です。 つまり、 **dbidexec** の値は **dbid**と同じになります。|  
|**uid**|**smallint**|アドホックなクエリ プランおよび使用可能になったプランのプラン作成者です。<br /><br /> -2 は、送られたバッチが暗黙的な名前解決に依存せず、複数ユーザー間での共有が可能なことを示します。 可能であればこの方法の使用をお勧めします。 他の値は、データベースのクエリを送っているユーザーのユーザー ID を示します。<br /><br /> ユーザーおよびロールの数が32767を超えた場合、オーバーフローまたは NULL を返します。|  
|**refcounts**|**int**|このキャッシュオブジェクトを参照している他のキャッシュオブジェクトの数。 1 は基になるオブジェクトであることを示します。|  
|**usecounts**|**int**|このキャッシュ オブジェクトが最初の時点から使用された回数です。|  
|**使用されたもの**|**int**|キャッシュ オブジェクトによって使用されたページ数です。|  
|**setopts**|**int**|コンパイル済みプランに影響する SET オプションの設定です。 この設定は、キャッシュ キーの一部です。 この列の値を変更すると、ユーザーが SET オプションを変更したことを示します。 ポリシーで設定できるオプションは、次のとおりです。<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**langid**|**smallint**|言語 ID。 キャッシュオブジェクトを作成した接続の言語の ID。|  
|**dateformat**|**smallint**|キャッシュオブジェクトを作成した接続の日付形式。|  
|**status**|**int**|キャッシュ オブジェクトがカーソル プランであるかどうかを示します。 現時点では、最下位ビットのみが使用されます。|  
|**lasttime**|**bigint**|これは旧バージョンとの互換性のためにだけ用意されています。 常に 0 を返します。|  
|**maxexectime**|**bigint**|これは旧バージョンとの互換性のためにだけ用意されています。 常に 0 を返します。|  
|**avgexectime**|**bigint**|これは旧バージョンとの互換性のためにだけ用意されています。 常に 0 を返します。|  
|**lastreads**|**bigint**|これは旧バージョンとの互換性のためにだけ用意されています。 常に 0 を返します。|  
|**lastwrites**|**bigint**|これは旧バージョンとの互換性のためにだけ用意されています。 常に 0 を返します。|  
|**sqlbytes**|**int**|プロシージャの定義または送信済みバッチのバイト長です。|  
|**server**|**nvarchar(3900)**|モジュール定義、または送信されたバッチの最初の3900文字。|  
  
## <a name="see-also"></a>参照  
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

