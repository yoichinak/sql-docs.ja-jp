---
description: 多対多リレーションシップの割り当て (Visual Database Tools)
title: 多対多リレーションシップ
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: afe40ef4863965905dedd825ee04bdb8a0e3e4d1
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038677"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>多対多リレーションシップの割り当て (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
多対多リレーションシップを使用すると、テーブルの各行を他のテーブルの複数の行と関連付けることができます。 たとえば、 `authors` テーブルと `titles` テーブルとの間に多対多リレーションシップを作成し、各著者をその全著作に対応付け、各著作をすべての著者に対応付けることができます。 一方のテーブルから一対多リレーションシップを作成すると、各著作には著者が 1 人しか存在しない、または各著者には 1 冊の著作しかないという情報が誤って示されることになります。  
  
テーブル間の多対多リレーションシップは、それぞれのデータベースで交差テーブルによって実現できます。 交差テーブルには、関連付ける 2 つのテーブルの各主キー列が格納されます。 これを使用して、2 つのテーブルの各主キー列から、交差テーブル内の対応する列へのリレーションシップを作成します。 pubs データベースでは、 `titleauthor` テーブルが交差テーブルです。  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>テーブル間で多対多リレーションシップを作成するには  
  
1.  データベース ダイアグラムで、多対多リレーションシップを作成する各テーブルを追加します。  
  
2.  ダイアグラムを右クリックし、ショートカット メニューの **[新しいテーブル]** をクリックして 3 つ目のテーブルを作成します。 これが交差テーブルになります。  
  
3.  **[名前の選択]** ダイアログ ボックスで、システムによって割り当てられたテーブル名を変更します。 たとえば、 `titles` テーブルと `authors` テーブルとの間の交差テーブルは、現在 `titleauthors`という名前です。  
  
4.  2 つのテーブルの各主キー列を交差テーブルにコピーします。 他の列も、他のテーブルに追加するのと同様に交差テーブルに追加できます。  
  
5.  交差テーブルで、他の 2 つのテーブルの主キーをすべて含めて主キーを設定します。 詳細については、[主キーの作成方法](../../relational-databases/tables/create-primary-keys.md)に関する記事を参照してください。  
  
6.  2 つの各主テーブルと交差テーブルとの間に一対多リレーションシップを定義します。 交差テーブルは、作成するリレーションシップの "多" 側に配置します。 詳細については、[テーブル間のリレーションシップの作成](../../relational-databases/tables/create-foreign-key-relationships.md)に関する記事を参照してください。  
  
    > [!NOTE]  
    > データベース ダイアグラムで交差テーブルを作成しても、関連テーブルから交差テーブルにデータは挿入されません。 テーブルにデータを挿入する方法については、「[方法 : 複製挿入クエリを作成する (Visual Database Tools)](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[データベース ダイアグラムの使用 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
