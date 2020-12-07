---
description: Oracle のテーブルおよび列の選択
title: Oracle のテーブルおよび列の選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d418e3d9f8b323c5f0c7905dad8c2ec636f1a3e0
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88457649"
---
# <a name="select-oracle-tables-and-columns"></a>Oracle のテーブルおよび列の選択

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [Oracle のテーブルおよび列の選択] ページを使用すると、変更をキャプチャする Oracle ソース データベースからテーブルを選択できます。 このページには次の要素があります。  
  
## <a name="options"></a>オプション  
 **テーブルの一覧**  
 テーブルの一覧には、次の 3 列が含まれています。  
  
-   **[Oracle テーブル名]**: テーブル スキーマを含むテーブルの名前です。  
  
-   **[キャプチャ インスタンス]**: インスタンス固有の変更データ キャプチャ オブジェクトを識別するために使用されるキャプチャ インスタンスの名前です。 キャプチャ インスタンスは NULL にできません。  
  
     指定しない場合、ソース スキーマ名とソース テーブル名に基づき、 `<schema-name>_<table-name>`形式の名前が付けられます。 キャプチャ インスタンス名は 100 文字を超えることはできず、データベース内で一意である必要があります。  
  
     この列のセルをクリックすると、 **capture_instance** を手動で編集できます。  
  
-   **[セキュリティ ロール]**: 変更データへのアクセスを制御するために使用されるデータベースのゲーティング ロールの名前です。  
  
     この列のセルをクリックすると、 **security_role** を手動で編集できます。  
  
 **テーブルの追加**  
 **[テーブルの追加]** をクリックすると、 [変更をキャプチャするための Oracle テーブルの選択](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)を行うことができる [テーブル選択] ダイアログ ボックスが開きます。  
  
 **[編集]**  
 一覧からテーブルを選択して **[編集]** をクリックすると、そのテーブルの **[プロパティ]** ダイアログ ボックスが表示され、 [変更をキャプチャするために選択したテーブルに対する変更](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)を行うことができます。  
  
 **Remove**  
 一覧からテーブルを選択して **[削除]** をクリックすると、CDC インスタンスからテーブルを削除できます。  
  
 適切なダイアログ ボックスを使用して [変更をキャプチャするための Oracle テーブルの選択](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md) または [変更をキャプチャするために選択したテーブルに対する変更](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md) を行った後、 **[次へ]** をクリックして [補足ログ スクリプトの生成および実行](../../integration-services/change-data-capture/generate-and-run-the-supplemental-logging-script.md)を行います。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [テーブルの編集](../../integration-services/change-data-capture/edit-tables.md)   
 [CDC へのテーブルの追加](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)   
 [テーブルのプロパティの編集](../../integration-services/change-data-capture/edit-the-table-properties.md)  
  
  
