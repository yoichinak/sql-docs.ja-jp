---
description: sysmergeschemachange (Transact-sql)
title: sysmergeschemachange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a53651fb604e9e0359857d8d7125faa47866f557
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540183"
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  スナップショット エージェントによって生成された、パブリッシュされたアーティクルに関する情報を格納します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|パブリケーションの ID です。|  
|**artid**|**uniqueidentifier**|アーティクルの ID です。|  
|**schemaversion**|**int**|前回のスキーマ変更の数。|  
|**schemaguid**|**uniqueidentifier**|前回のスキーマの一意な ID。|  
|**schematype**|**int**|スキーマ変更の種類。<br /><br /> **-1** = 無効です。<br /><br /> **1** = SQL コマンド。<br /><br /> **2** = スキーマスクリプト。<br /><br /> **3** = ネイティブな一括コピープログラムユーティリティ (BCP)。<br /><br /> **4** = 文字 BCP。<br /><br /> **5** = 最後に記録された生成。<br /><br /> **6** = 最後に送信された生成。<br /><br /> **7** = ディレクトリ。<br /><br /> **8** = 優先順位。<br /><br /> **9** = 保有期間。<br /><br /> **10** = トリガースクリプト。<br /><br /> **11** = Alter table。<br /><br /> **12** = すべて再初期化します。<br /><br /> **13** = ALTER TABLE (以外 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )<br /><br /> **14** = upload を使用して再初期化します。<br /><br /> **15** = 制約とインデックススクリプト。<br /><br /> **16** = メタデータのクリーンアップ。<br /><br /> **17** = 最後に送信された生成結果を更新します。<br /><br /> **18** = 下位互換性レベル。<br /><br /> **19** = サブスクライバー情報を検証します。<br /><br /> **20** = 適切なパーティション分割。<br /><br /> **21** = カスタム競合回避モジュール。<br /><br /> **22** = アーティクルの処理順序。<br /><br /> **23** = トランザクションパブリケーションでパブリッシュされました。<br /><br /> **24** = エラーを補正します。<br /><br /> **25** = 代替スナップショットフォルダー。<br /><br /> **26** = ダウンロード専用。<br /><br /> **27** = 削除の追跡。<br /><br /> **40** = 作成前のスナップショットスクリプト。<br /><br /> **45** = 作成後のスナップショットスクリプト。<br /><br /> **46** = オンデマンドユーザースクリプト。<br /><br /> **50** = スナップショットヘッダーを開始します。<br /><br /> **51** = スナップショットヘッダーの終了。<br /><br /> **52** = スナップショットトレーラー。<br /><br /> **53** = ファイル転送プロトコル (FTP) アドレス。<br /><br /> **54** = FTP ポート。<br /><br /> **55** = FTP サブディレクトリ。<br /><br /> **56** = スナップショットは圧縮されています。<br /><br /> **57** = FTP ログイン。<br /><br /> **58** = FTP パスワード。<br /><br /> **60** = システムの事前作成スクリプト。<br /><br /> **61** = ストアドプロシージャスキーマ。<br /><br /> **62** = ビュースキーマ。<br /><br /> **63** = ユーザー定義関数スキーマ。<br /><br /> **64** = インデックスを表示します。<br /><br /> **65** = 拡張プロパティ。<br /><br /> **66** = Validate。<br /><br /> **67** = スナップショット前の SQL コマンド。<br /><br /> **71** = 動的スナップショット検証。<br /><br /> **80** = システムテーブルネイティブ BCP 9.0。<br /><br /> **81** = システムテーブル文字 BCP 9.0。<br /><br /> **82** = システムテーブルネイティブ BCP 9.0 (グローバルのみ)。<br /><br /> **83** = システムテーブル文字 BCP 9.0 (グローバルのみ)。<br /><br /> **84** = システムテーブルネイティブ BCP 9.0 (ライトウェイト)。<br /><br /> **85** = システムテーブル文字 BCP 9.0 (簡易)。<br /><br /> **128** = 動的 BCP (ビット)。<br /><br /> **131** = 動的なネイティブ BCP。<br /><br /> **132** = 動的な文字 BCP。<br /><br /> **208** = 動的システムテーブルネイティブ BCP 9.0。<br /><br /> **209** = 動的システムテーブル文字 BCP 9.0。<br /><br /> **210** = 動的システムテーブルネイティブ BCP 9.0 (グローバルのみ)。<br /><br /> **211** = 動的システムテーブル文字 BCP 9.0 (グローバルのみ)。<br /><br /> **212** = 動的システムテーブルネイティブ BCP 9.0 (簡易)。<br /><br /> **213** = 動的システムテーブル文字 BCP 9.0 (簡易)。<br /><br /> **300** = データ定義言語 (DDL) アクション。<br /><br /> **1024** = 増分スナップショットコントロール。<br /><br /> **1049** = 増分スナップショットフォルダー。<br /><br /> **1074** = 増分スナップショットの開始ヘッダーです。<br /><br /> **1075** = 増分スナップショットの終了ヘッダー。<br /><br /> **1076** = 増分スナップショットトレーラー。<br /><br /> **1077** = 増分 FTP アドレス。<br /><br /> **1078** = 増分 FTP ポート。<br /><br /> **1079** = 増分 FTP サブディレクトリ。<br /><br /> **1080** = 増分圧縮スナップショット。<br /><br /> **1081** = 増分 FTP ログイン。<br /><br /> **1082** = 増分 FTP パスワード。|  
|**スキーマのスキーマ**|**nvarchar (2000)**|スクリプトファイルの名前、またはファイル名を含むコマンド|  
|**schemastatus**|**tinyint**|アーティクルに対してスキーマ変更が保留されているかどうかを示します。次のいずれかの値を指定できます。<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = アクティブ。<br /><br /> スキーマ変更が保留中の場合、この値は **1**に設定されます。|  
|**schemasubtype**|**int**|スキーマ変更のサブタイプ。<br /><br /> **1** = addcolumn<br /><br /> **2** = dropcolumn<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = addprimarykey<br /><br /> **5** = addunique<br /><br /> **6** = addreference<br /><br /> **7** = dropconstraint<br /><br /> **8** = adddefault<br /><br /> **9** = addcheck<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
