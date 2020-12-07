---
description: データベース ダイアグラム デザイナーの設定 (Visual Database Tools)
title: データベース ダイアグラム デザイナーの設定
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 09750a9c500c0c5928924845f883acfc2a836917
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034866"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>データベース ダイアグラム デザイナーの設定 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
データベース ダイアグラム デザイナーを使用するには、 **db_owner** ロールのメンバーによって、ダイアグラムへのアクセスを制御するようにあらかじめ設定しておく必要があります。  
  
### <a name="to-set-up-database-diagramming"></a>データベース ダイアグラムを設定するには  
  
1.  オブジェクト エクスプローラーから、データベース ノードを展開します。  
  
2.  データベース接続のデータベース ダイアグラム ノードを展開します。  
  
3.  データベースのダイアグラム化を設定するかどうかをたずねるメッセージが表示されたら、 **[はい]** を選択します。  
  
    > [!NOTE]  
    > これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにデータベース ダイアグラム テーブル、システム ストアド プロシージャ、およびシステム関数が作成されます。  
  
4.  Visual Studio では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに次のオブジェクトが作成されます。  
  
    1.  sysdiagrams テーブル  
  
    2.  sp_alterdiagram ストアド プロシージャ  
  
    3.  sp_creatediagram ストアド プロシージャ  
  
    4.  sp_dropdiagram ストアド プロシージャ  
  
    5.  sp_renamediagram ストアド プロシージャ  
  
    6.  fn_diagramobjects 関数  
  
    7.  sp_helpdiagrams ストアド プロシージャ  
  
    8.  sp_helpdiagramsdefinition ストアド プロシージャ  
  
    9. sp_upgraddiagrams ストアド プロシージャ  
  
## <a name="see-also"></a>関連項目  
[データベース ダイアグラムの所有権について (Visual Database Tools)](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[旧エディションのデータベース ダイアグラムのアップグレード (Visual Database Tools)](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)  
