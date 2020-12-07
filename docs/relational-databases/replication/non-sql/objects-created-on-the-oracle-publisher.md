---
description: Oracle パブリッシャー上で作成されたオブジェクト
title: Oracle パブリッシャー上で作成されたオブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 744cf1e5878382e1eae804b4705e21d1fa21d098
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420456"
---
# <a name="objects-created-on-the-oracle-publisher"></a>Oracle パブリッシャー上で作成されたオブジェクト
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションでは、変更の追跡と転送を行えるように、Oracle パブリッシャーにデータベース オブジェクトがインストールされます ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって Oracle パブリッシャーにバイナリ ファイルがインストールされることはありません)。 次の表に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで Oracle パブリッシャーがパブリッシャーとして認識されたときに、Oracle パブリッシャーで作成されるオブジェクトの一覧を示します。 オブジェクトの説明は、情報の提供のみを目的としています。 これらのオブジェクトは変更しないでください。  
  
|オブジェクト名|オブジェクトの型|説明|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|テーブル|パブリッシュされたテーブルが変更されたときに情報を格納するために使用する変更追跡テーブル。 変更追跡テーブルは、パブリッシュされたテーブルごとに作成されます。|  
|HREPL_Changes|テーブル|トランザクション セットに割り当てられるのを待機している変更の数を判断するために、Xactset ジョブによって内部的に使用されるテーブル。 このジョブの詳細については、「[Oracle パブリッシャーのパフォーマンス チューニング](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)」を参照してください。|  
|HREPL_Distributor|テーブル|Oracle パブリッシャーに関連付けられた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターに関する情報を保持するディストリビューター状態テーブル。|  
|HREPL_Event|テーブル|スナップショットと行数要求とを同期するために使用されるイベント テーブル。|  
|HREPL_Mutex|テーブル|ログ リーダー エージェントとデータベース ジョブが、Oracle パッケージ プロシージャ PopulatePollTable を同時に実行しないようにするために使われるテーブル。|  
|HREPL_Poll|テーブル|パブリッシュされたテーブルに対する一連の変更に関連付けられたログ テーブル エントリを識別するために使われるテーブル。|  
|HREPL_PublishedTables|テーブル|トランザクション パブリケーション内の各アーティクルのエントリを含むテーブル。|  
|HREPL_Publisher|テーブル|パブリッシャー固有の情報を保持するために使われるパブリッシャー状態テーブル。|  
|HREPL_SchemaFilter|テーブル|パブリケーションの新規作成ウィザードでパブリッシュする際に表示されないスキーマを格納するテーブル。|  
|HREPL_XactsetCreateTimes|テーブル|各トランザクション設定に関連付けられた作成時刻を特定するテーブル。|  
|HREPL_XactsetJob|テーブル|Xactset ジョブの現在のパラメーター設定が格納されているテーブル。|  
|HREPL_Pollid|シーケンス|ポーリング ID を生成するために使われるシーケンス。|  
|HREPL_Seq|シーケンス|変更コマンドを順序付けるために使われるシーケンス。|  
|HREPL_Stmt|シーケンス|ステートメント ID を生成するために使われるシーケンス。|  
|HREPL|パッケージとパッケージ本体|パブリッシャーで作成された、パブリッシャー サポート コードのパッケージ。|  
|MSSQLSERVERDISTRIBUTOR|パブリック シノニム|HREPL_Distributor テーブル用のパブリック シノニム。 Oracle パブリッシャーを使用するようにディストリビューターを構成すると、このシノニムが既にデータベースにある場合に、削除されてから再作成されます。<br /><br /> パブリック シノニムと、CASCADE オプションで構成した Oracle レプリケーション ユーザーを削除すると、Oracle パブリッシャーからすべてのレプリケーション オブジェクトが削除されます。|  
|HREPL_Len_I_J_K|機能|Oracle パブリッシング パッケージ コードの外で定義された関数。LONG 列の長さに対するクエリを実行するために使用します (パブリッシュされた LONG 列を含むテーブルに対してパラメーター化されたコマンドを生成する際に使用されます)。 関数は、LONG 列を含むパブリッシュされたテーブルごとに作成されます。|  
|HREPL_DropPublisher|手順|Oracle パブリッシング パッケージ コードの外で定義されたプロシージャで、Oracle パブリッシャーを削除するために使用します。|  
|HREPL_ExecuteCommand|手順|Oracle パブリッシング パッケージ コードの外で定義されたプロシージャで、パブリッシャーでコマンドを実行するために使用します。|  
|HREPL_ArticleN_Trigger_Row|トリガー|パブリッシュされたテーブルごとに生成されるトリガーで、行の変更を追跡するために使用します。|  
|HREPL_ArticleN_Trigger_Stmt|トリガー|パブリッシュされたテーブルごとに生成されるトリガーで、ステートメント レベルの変更を追跡するために使用します。|  
|HREPL_Article_I_J|View|パブリッシュされたテーブルごとに作成されるビューで、パブリッシュされたテーブルにクエリを実行するために使用されます。|  
|HREPL_Log_I_J_K|View|パブリッシュされたテーブルごとに作成されるビューで、変更追跡テーブルにクエリを実行するために使用されます。|  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーの構成](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle パブリッシングの用語](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle パブリッシングの概要](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
