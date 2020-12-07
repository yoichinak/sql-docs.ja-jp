---
description: DML トリガー
title: DML トリガー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27776324d94176619c25acbeefb3b6bd901d8a2a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418936"
---
# <a name="dml-triggers"></a>DML トリガー
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  DML トリガーとは、そこに定義されているテーブルまたはビューに影響するようなデータ操作言語 (DML) イベントが発生すると自動的に実行される特殊なストアド プロシージャです。 DML イベントには、INSERT、UPDATE、または DELETE のステートメントが含まれます。 DML トリガーを使用して、ビジネス ルールやデータの整合性を強制的に適用したり、他のテーブルを照会したりできるほか、複雑な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用することもできます。 トリガーとそのトリガーを起動するステートメントは単一のトランザクションとして扱われ、このトランザクションはトリガー内からロールバックできます。 ディスクの空き容量の不足などの重大なエラーが検出されると、このトランザクション全体が自動的にロールバックされます。  
  
## <a name="dml-trigger-benefits"></a>DML トリガーの利点  
 エンティティの整合性またはドメインの整合性を適用できるという点で、DML トリガーは制約に似ています。 一般に、PRIMARY KEY 制約と UNIQUE 制約の一部であるインデックス、またはこれらの制約とは無関係に作成されたインデックスの最下位レベルで、エンティティの整合性を常に確保する必要があります。 ドメインの整合性の確保には CHECK 制約を使用し、参照整合性 (RI) の確保には FOREIGN KEY 制約を使用する必要があります。 DML トリガーは、制約でサポートされている機能がアプリケーションの機能要件を満たすことができない場合に最も役立ちます。  
  
 以下に DML トリガーと制約を比較し、どのような場合に DML トリガーが有利となるかを示します。  
  
-   DML トリガーでは、データベースの関連テーブルを使用して変更を連鎖することができます。ただし、連鎖参照整合性制約を使用すると、これらの変更をより効率的に実行できます。 REFERENCES 句によって連鎖参照動作が定義されていない場合、FOREIGN KEY 制約で検証できるのは、ある列の値が別の列の値と完全に一致しているかどうかだけです。  
  
-   DML トリガーを使用すると、不適切あるいは悪意のある INSERT、UPDATE、および DELETE 操作から保護できます。また、CHECK 制約を使用して定義された制約よりも複雑な制約を適用することができます。  
  
     CHECK 制約とは異なり、DML トリガーでは、他のテーブルの列を参照できます。 たとえば、トリガーでは、他のテーブルに対して SELECT ステートメントを使用して、挿入または更新されたデータと比較したり、データの変更やユーザー定義のエラーメッセージの表示などの追加処理を実行することができます。  
  
-   DML トリガーを使用して、データの変更前と変更後のテーブルの状態を評価し、その違いに基づいた操作を実行することもできます。  
  
-   1 つのテーブルに同じ種類 (INSERT、UPDATE、または DELETE) の DML トリガーを複数作成すると、1 つの変更ステートメントに対して複数の異なる操作を実行できます。  
  
-   制約でエラーを通知するには、標準化されたシステム エラー メッセージを使用する必要があります。 カスタマイズしたメッセージや複雑なエラー処理が必要な場合、またはこれらを使用する利点がある場合は、アプリケーションでは、トリガーを使用する必要があります。  
  
-   DML トリガーでは参照整合性に反する変更を禁止してロールバックすることができるので、実行されたデータ変更を取り消すことができます。 このようなトリガーは、外部キーを変更したときに、新しい値がその主キーに一致しない場合に実行されます。 ただし、通常、この目的には FOREIGN KEY 制約を使用します。  
  
-   トリガー テーブルに制約が存在する場合、これらの制約は、INSTEAD OF トリガーが実行されてから、AFTER トリガーが実行されるまでの間にチェックされます。 制約違反の場合は、INSTEAD OF トリガー動作がロールバックされ、AFTER トリガーは実行されません。  
  
## <a name="types-of-dml-triggers"></a>DML トリガーの種類  
 AFTER トリガー  
 AFTER トリガーは、INSERT、UPDATE、MERGE、または DELETE ステートメントの動作が実行された後に実行されます。 制約違反が発生した場合は、AFTER トリガーは実行されません。したがってこのトリガーは、制約違反を防ぐための処理には使用できません。 MERGE ステートメントで指定されたすべての INSERT、UPDATE、または DELETE 操作について、対応するトリガーが各 DML 操作に対して実行されます。  
  
 INSTEAD OF トリガー  
 INSTEAD OF トリガーは、トリガーを起動するステートメントの標準動作をオーバーライドする働きをします。 たとえば、このトリガーを使用して、1 つ以上の列に対するエラー チェックや値チェックを実行することができます。行の挿入、更新、削除などの操作の前に追加の処理を実行することが可能です。 たとえば、経理テーブル内の時給列の値を更新するときに、更新する値が指定された値を超えている場合は、エラー メッセージを生成してトランザクションをロールバックするようにトリガーを定義することができます。また、新しいレコードを経理テーブルに挿入する前に監査記録にそのレコードを挿入するようにトリガーを定義することもできます。 INSTEAD OF トリガーを使用する主な利点は、更新可能ではなかったビューを更新できるようになることです。 たとえば、複数のベース テーブルに基づいたビューでは、INSTEAD OF トリガーを使用して、複数のテーブルのデータを参照する挿入、更新、および削除の各操作をサポートする必要があります。 INSTEAD OF トリガーのもう 1 つの利点は、バッチの一部を拒否しながらバッチのその他の部分を正常に実行できるロジックをコード化できることです。  
  
 次の表は、AFTER トリガーと INSTEAD OF トリガーの機能を比較したものです。  
  
|機能|AFTER トリガー|INSTEAD OF トリガー|  
|--------------|-------------------|------------------------|  
|適用範囲|テーブル|テーブルとビュー|  
|テーブルまたはビューごとの数|トリガーを起動する動作 (UPDATE、DELETE、および INSERT) ごとに複数指定できます。|トリガーを起動する動作 (UPDATE、DELETE、および INSERT) ごとに 1 つしか指定できません。|  
|連鎖参照|制限はありません。|INSTEAD OF UPDATE トリガーと DELETE トリガーは、参照整合性制約の連鎖の対象となっているテーブルでは許可されません。|  
|実行|次の処理の後<br /><br /> 制約処理<br /><br /> 宣言参照動作<br /><br /> **inserted** テーブルと **deleted** テーブルの作成<br /><br /> トリガーを起動する動作|次の処理の前: 制約処理<br /><br /> 次の処理の代わり: トリガーを起動する動作<br /><br /> 次の処理の後:  **inserted** テーブルと **deleted** テーブルの作成|  
|実行の順序|最初と最後の実行内容を指定できます。|適用なし|  
|**inserted**テーブルと **deleted**テーブル内の **varchar(max)** 、 **nvarchar(max)** 、および **varbinary(max)** の列参照|許可|許可|  
|**inserted**テーブルと **deleted**テーブル内の **text** 、 **ntext** 、および **image** の列参照|使用できません|許可|  
  
 CLR トリガー  
 CLR トリガーは、AFTER トリガーと INSTEAD OF トリガーのいずれかにすることができます。 また、CLR トリガーは DDL トリガーにすることもできます。 CLR トリガーは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを実行するのではなく、.NET Framework で作成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアップロードされたアセンブリのメンバーであるマネージド コードに記述されている、1 つ以上のメソッドを実行します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|トピック|  
|----------|-----------|  
|DML トリガーの作成方法について説明します。|[DML トリガーの作成](../../relational-databases/triggers/create-dml-triggers.md)|  
|CLR トリガーの作成方法について説明します。|[CLR トリガーの作成](../../relational-databases/triggers/create-clr-triggers.md)|  
|単一行および複数行のデータ変更を処理する DML トリガーの作成方法について説明します。|[複数行のデータを処理するための DML トリガーの作成](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|トリガーを入れ子にする方法について説明します。|[入れ子になったトリガーの作成](../../relational-databases/triggers/create-nested-triggers.md)|  
|AFTER トリガーの起動順序を指定する方法について説明します。|[最初と最後のトリガーの指定](../../relational-databases/triggers/specify-first-and-last-triggers.md)|  
|トリガー コードの中で特殊な inserted テーブルおよび deleted テーブルを使用する方法について説明します。|[inserted テーブルと deleted テーブルの使用](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)|  
|DML トリガーに変更を加えたり名前を変更する方法について説明します。|[DML トリガーの変更または名前の変更](../../relational-databases/triggers/modify-or-rename-dml-triggers.md)|  
|DML トリガーに関する情報を表示する方法について説明します。|[DML トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-dml-triggers.md)|  
|DML トリガーを削除または無効化する方法について説明します。|[DML トリガーの削除または無効化](../../relational-databases/triggers/delete-or-disable-dml-triggers.md)|  
|トリガーのセキュリティを管理する方法について説明します。|[トリガーのセキュリティの管理](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [トリガー関数 &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-functions-transact-sql.md)  
  
  
