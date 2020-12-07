---
description: 外部キー リレーションシップの変更
title: 外部キー リレーションシップの変更 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65538
- vdt.ppg.relationships
helpviewer_keywords:
- foreign keys [SQL Server], modifying
- modifying foreign keys
ms.assetid: 0c9ca80d-d79b-44c4-a21e-0fce39c398ec
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1c8972b0f407f7de3a4fa6f825e6a1b2b0d33953
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645912"
---
# <a name="modify-foreign-key-relationships"></a>外部キー リレーションシップの変更

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、リレーションシップの外部キー側を変更できます。 テーブルの外部キーを変更すると、主キー テーブルの列に関連付けられる列が変更されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用して外部キーを変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
 新しい外部キー列は、関連付けられる主キー列のデータ型およびサイズと一致する必要があります。ただし、次の例外があります。  
  
-   **char** 列または **sysname** 列は **varchar** 列と関連付けることができます。  
  
-   **binary** 列は **varbinary** 列と関連付けることができます。  
  
-   alias データ型は、その基本型に関連付けることができます。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-a-foreign-key"></a>外部キーを変更するには  
  
1.  **オブジェクト エクスプローラー**で、外部キーが含まれているテーブルを展開し、 **[キー]** を展開します。  
  
2.  変更する外部キーを右クリックし、 **[変更]** を選択します。  
  
3.  **[外部キー リレーションシップ]** ダイアログ ボックスでは、次の変更を行うことができます。  
  
     **[選択されたリレーションシップ]**  
     既存のリレーションシップを一覧表示します。 右側のグリッドにプロパティを表示するリレーションシップを選択します。 この一覧が空の場合、テーブルにはリレーションシップがまったく定義されていません。  
  
     **追加**  
     新しいリレーションシップを作成します。 リレーションシップを有効にする前に、 **[テーブルと列の指定]** を設定する必要があります。  
  
     **削除**  
     **[選択されたリレーションシップ]** ボックスの一覧で選択したリレーションシップを削除します。 追加したリレーションシップを取り消すには、このボタンを使用してリレーションシップを削除します。  
  
     **[全般] カテゴリ**  
     展開して **[作成時または再度有効化するときに既存データを確認]** および **[テーブルと列の指定]** を表示します。  
  
     **[作成時または再度有効化するときに既存データを確認]**  
     制約を作成した時点、または制約を再度有効にした時点よりも前からテーブルに存在しているすべてのデータについて、その制約に対して検証します。  
  
     **[テーブルと列の指定] カテゴリ**  
     展開すると、リレーションシップの外部キーおよび主キー (一意キー) として、どのテーブルのどの列が機能しているかわかります。 これらの値を編集または定義するには、プロパティ フィールドの右にある省略記号ボタン ( **[...]** ) をクリックします。  
  
     **[外部キーの基本テーブル]**  
     選択したリレーションシップで、どのテーブルが外部キーとして機能する列を含んでいるかを示します。  
  
     **[外部キー列]**  
     選択したリレーションシップで、どの列が外部キーとして機能しているかを示します。  
  
     **[主/一意キーの基本テーブル]**  
     選択したリレーションシップで、どのテーブルが主キー (一意キー) として機能する列を含んでいるかを示します。  
  
     **[主/一意キー列]**  
     選択したリレーションシップで、どの列が主キー (一意キー) として機能しているかを示します。  
  
     **[IDENTITY] カテゴリ**  
     展開して **[オブジェクト名]** および **[説明]** のプロパティ フィールドを表示します。  
  
     **名前**  
     リレーションシップの名前を表示します。 新しいリレーションシップを作成した場合、このプロパティには、 **テーブル デザイナー**のアクティブ ウィンドウのテーブルに基づいて、既定の名前が設定されます。 名前はいつでも変更できます。  
  
     **説明**  
     リレーションシップの説明です。 より詳細な説明を記述する場合は、 **[説明]** をクリックしてから、プロパティ フィールドの右に表示される省略記号 ( **[...]** ) をクリックします。 これにより、テキストを書くことができる領域が大きくなります。  
  
     **[テーブル デザイナー] カテゴリ**  
     展開して **[作成時または再度有効化するときに既存データを確認]** および **[レプリケーションに対して適用]** に関する情報を表示します。  
  
     **[レプリケーションに対して適用]**  
     レプリケーション エージェントがこのテーブルに対して挿入、更新、または削除操作を行うときに制約を適用するかどうかを示します。  
  
     **[外部キーの制約を適用]**  
     リレーションシップの列のデータに対する変更が、外部キー リレーションシップの整合性に違反しているときに、その変更を許可するかどうかを示します。 このような変更を許可する場合には **[はい]** を、許可しない場合には **[いいえ]** をクリックします。  
  
     **[INSERT および UPDATE の指定] カテゴリ**  
     展開して、そのリレーションシップの **[DeleteRule の設定]** および **[UpdateRule の設定]** に関する情報を表示します。  
  
     **[DeleteRule の設定]**  
     外部キー リレーションシップに関連するデータを持つ行をユーザーが削除しようとした場合の処理を指定します。  
  
    -   **[動作なし]** &#xA0;&#xA0;&#xA0;削除操作が許可されていないことをユーザーに通知するエラー メッセージが出力され、DELETE がロールバックされます。  
  
    -   **[重ねて表示]** &#xA0;&#xA0;&#xA0;外部キー リレーションシップに関係するデータを含む行がすべて削除されます。 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。  
  
    -   **[Null に設定]** テーブルのすべての外部キー列が null 値を使用できる場合、null 値が設定されます。  
  
    -   **[既定値の設定]** テーブルのすべての外部キー列に既定値が定義されている場合、既定値が設定されます。  
  
     **[UpdateRule の設定]**  
     外部キー リレーションシップに関連するデータを持つ行をユーザーが更新しようとした場合の処理を指定します。  
  
    -   **[動作なし]** &#xA0;&#xA0;&#xA0;更新操作が許可されていないことをユーザーに通知するエラー メッセージを出力し、UPDATE がロールバックします。  
  
    -   **[重ねて表示]** &#xA0;&#xA0;&#xA0;外部キー リレーションシップに関係するデータを含む行がすべて更新されます。 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。  
  
    -   **[Null に設定]** テーブルのすべての外部キー列が null 値を使用できる場合、null 値が設定されます。  
  
    -   **[既定値の設定]** &#xA0;&#xA0;テーブルのすべての外部キー列に既定値が定義されている場合、その列に定義されている既定値が設定されます。  
  
4.  **[ファイル]** メニューの **[_<テーブル名>_ を保存]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 **外部キーを変更するには**  
  
 Transact-SQL を使用して FOREIGN KEY 制約を変更するには、まず既存の FOREIGN KEY 制約を削除してから、新しい定義を使用して再作成する必要があります。 詳細については、「 [Delete Foreign Key Relationships](../../relational-databases/tables/delete-foreign-key-relationships.md) 」および「 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
