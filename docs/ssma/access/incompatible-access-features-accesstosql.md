---
title: 互換性のないアクセス機能 (アクセス機能) |Microsoft Docs
description: SQL Server と互換性のない Access database 機能に関する移行の問題とその対処方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4ecf50e11bab0d6e1034299cba87c40137556505
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985148"
---
# <a name="incompatible-access-features-accesstosql"></a>互換性のないアクセス機能 (Access Stosql)
Access データベースのすべての機能がと互換性があるわけではありません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 たとえば、とのアクセスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 予約されたキーワードのセットが異なります。 これらの問題により、への移行が成功することが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ありません。 移行に関する問題とその対処方法については、次の表を参照してください。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>移行に影響する可能性のあるデータベースの設定または機能  
  
|Access データベースの設定または機能|移行に関する問題|  
|--------------------------------------|-------------------|  
|Access テーブルには一意のインデックスがありません。|一意のインデックスを持たないテーブルをに移行する場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行後にテーブルを変更することはできません。 これにより、アプリケーションの互換性の問題が発生する可能性があります。<br /><br />Access データベースオブジェクトを変換すると、[出力] ウィンドウに、一意のインデックスのない Access テーブルが一覧表示されます。<br /><br />変換時にテーブルに主キーを追加するようにアクセスを構成でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [プロジェクトの設定 (変換)](./project-settings-conversion-accesstosql.md)」を参照してください。|  
|Access テーブルにはレプリケーション列があります。|レプリケーションシステム列を含む Access テーブルをに移行すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行後に Jet レプリケーション機能が破損します。<br /><br />移行後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの同期されたコピーを維持するには、レプリケーションの使用を検討してください。|  
|一意のインデックスを持つ Access テーブルには、複数の null 値が含まれます。|複数の null 値を持つ一意のインデックスを持つアクセステーブルは、に転送できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。では、一意のインデックスで複数の null 値が許可されないため [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。 これらのテーブルの移行は失敗します。<br /><br />SSMA は、この問題に対して評価レポートでのフラグを作成します。 評価レポートを作成するには、「 [変換するアクセスデータベースオブジェクトの評価](assessing-access-database-objects-for-conversion-accesstosql.md)」を参照してください。<br /><br />この問題が存在する場合は、主キーに重複する null 値が含まれていないことを確認する必要があります。 または、複数の null 値を含む主キーまたは一意のインデックスを削除する必要があります。|  
|Access テーブルには、範囲外の日付値が含まれて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] います。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime**型は、1 Jan 1753 から 31 Dec 9999 の範囲の日付のみを受け取ります。 Access では、1 Jan 100 ~ 31 Dec 9999 の範囲の日付を受け付けます。<br /><br />SSMA は、この問題に対して評価レポートでのフラグを作成します。 評価レポートを作成するには、「 [変換するアクセスデータベースオブジェクトの評価](assessing-access-database-objects-for-conversion-accesstosql.md)」を参照してください。<br /><br />SSMA が範囲外の日付を解決する方法を構成でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-accesstosql.md)」を参照してください。|  
|アクセスのインデックス長が900バイトを超えています。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスでは、インデックスキー列の合計サイズに900バイトの制限があります。 Access テーブルでより大きなインデックスが使用されている場合は、SSMA によって警告が表示されます。<br /><br />データの移行を続行した場合、移行が失敗する可能性があります。|  
|アクセスオブジェクト名は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キーワードであるか、特殊文字を含んでいます。|にアクセスし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] さまざまな予約済みキーワードと特殊文字セットを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、キーワードを使用して名前が付けられたオブジェクト、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "select" や "select" などの引用符で囲まれた識別子を使用する場合は、特殊文字を含むオブジェクトを受け入れます。 詳細については、オンラインブックの「区切られた識別子 (データベースエンジン)」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />**注:** 識別子を区切るために引用符を使用するには QUOTED_IDENTIFIER を ON に設定する必要があります。<br /><br />たとえば、 `CREATE TABLE [schema](c1 [FOR])` は、 **スキーマ** と **に** 予約されているキーワードであっても、有効なステートメントです。 また、 `CREATE TABLE [xxx*yyy](c1 x&y)` テーブルと列の名前に特殊文字** \& #42;** およびが含まれている場合でも、は有効なステートメントです **&amp;** 。<br /><br />これらのオブジェクトを参照するすべてのクエリでも、角かっこまたは引用符で囲まれた名前を使用する必要があります。 たとえば、クエリは `SELECT * FROM schema` 失敗します。 正しいクエリは次のとおりです `SELECT * FROM [schema]` 。<br /><br />Access データベースオブジェクトを変換すると、[出力] ウィンドウに、キーワードまたは特殊文字を使用する Access テーブルが一覧表示されます。 Access のテーブルを変更してから、データベースを削除してから再度追加することができます。または、これらのオブジェクトを参照するクエリを変更して、クエリが識別子を区切るために角かっこまたは引用符を使用するようにすることもできます。 クエリを変更しないと、Access アプリケーションからエラーが返されるか、他の問題が発生する可能性があります。|  
|主キー/外部キーのリレーションシップでは、フィールドのサイズが異なります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、外部キー制約が設定されているデータ型やサイズが異なる列をリンクする Jet 機能はサポートされていません。<br /><br />Access データベースオブジェクトを変換すると、に変換されない主キー/外部キーの制約が出力ウィンドウに一覧表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 アクセス列のデータ型とサイズを変更して、access データベースを削除してから再度追加することができます。 または、データを移行することもできますが、ではこれらの制約は作成されません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|アクセスリレーションシップ内の参照されているテーブルには、主キーと一意のインデックスのいずれもありません。|アクセスは、参照されるテーブルに主キーまたは一意のインデックスがないテーブル間のリレーションシップを受け入れます。 ただし、これはではサポートされていません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />Access データベースオブジェクトを変換すると、[出力] ウィンドウにはリレーションシップがあり、主キーまたは一意のインデックスがないテーブルが一覧表示されます。 テーブルを変更して主キーまたは一意のインデックスを追加し、Access データベースを削除してから追加し直すことができます。 または、テーブル間のリレーションシップが壊れていても、データを移行できます。|  
|Access テーブルにはハイパーリンク列があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **ハイパーリンク** 列をサポートしていません。 代わりに、列は Access memo 列と同じように扱われます。 既定では、これらの列はの **nvarchar (max)** 列に変換され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 マッピングはカスタマイズできます。 詳細については、「 [ソースとターゲットのデータ型のマッピング](mapping-source-and-target-data-types-accesstosql.md)」を参照してください。|  
|既定値または検証規則の式には、または SQL Azure に変換できないアクセス関数が含まれて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] います。|既定の式や検証規則にアクセスするには、アクセスシステム関数、またはにマップされていないユーザー定義関数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure します。 または SQL Azure に割り当てられていない関数を使用すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、既定の式や検証規則をまたは SQL Azure に読み込むことができなくなり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
  
## <a name="see-also"></a>参照  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
