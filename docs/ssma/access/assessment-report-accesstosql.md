---
description: 評価レポート (Sql server による)
title: 評価レポート (Sql server による) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6c747f50c9216626e710318175cf5e53a0624d7a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987658"
---
# <a name="assessment-report-accesstosql"></a>評価レポート (Sql server による)
[評価レポート] ウィンドウには、データベースオブジェクトを構文に変換した結果が表示され [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。また、移行プロジェクトの複雑さとコストを見積もるのにも役立ちます。  
  
評価レポートを作成するには、ソースメタデータエクスプローラーで変換するオブジェクトを選択し、[ **データベース**] を右クリックして、[ **レポートの作成**] を選択します。 スキーマを変換した後に、このレポートを自動的に表示することもできます。 ただし、レポート名は変換レポートになります。 詳細については、「 [プロジェクトの設定 (GUI) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md)」を参照してください。  
  
## <a name="options"></a>オプション  
**エクスプローラー ペイン**  
評価レポートのオブジェクトの階層が含まれます。 [フォルダー] を展開して、個々のオブジェクトとサブコンポーネントを表示します。 カテゴリまたはオブジェクトをクリックすると、そのカテゴリまたはオブジェクトの変換統計が詳細ウィンドウに表示されます。  
  
**詳細ウィンドウ**  
選択したオブジェクトの変換の統計情報またはエラーと警告メッセージを表示します。 たとえば、[テーブル] フォルダーを選択した場合、[詳細] ペインには、変換された外部キー、インデックス、主キー、およびテーブルの数が表示されます。  
  
**メッセージ ペイン (Messages pane)**  
評価レポートの作成時に生成されたエラー、警告、および情報メッセージを表示します。 メッセージは数値でグループ化されます。  
  
メッセージの詳細を表示するには、[ **エラー**]、[ **警告**]、または [ **メッセージ**] をクリックし、メッセージを展開します。 SSMA には、このエラーが発生したオブジェクトの一覧が表示されます。 オブジェクトをクリックすると、そのオブジェクトのすべての変換の詳細が表示されます。  
  
## <a name="see-also"></a>参照  
[ユーザーインターフェイスリファレンス (アクセス)](./user-interface-reference-accesstosql.md)  
