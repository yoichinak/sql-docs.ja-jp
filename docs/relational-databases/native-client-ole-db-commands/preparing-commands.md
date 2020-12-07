---
description: SQL Server Native Client でのコマンドの準備
title: コマンドの準備 (Native Client OLE DB プロバイダー)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8119cf7e254d4d016b21b9a2aeaa976121df8703
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455822"
---
# <a name="preparing-commands-in-sql-server-native-client"></a>SQL Server Native Client でのコマンドの準備
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、1 つのコマンドを最適化された状態で複数回実行できるように、コマンドを準備できます。ただし、コマンドを準備することでオーバーヘッドが生じるので、コンシューマーではコマンドを 2 回程度実行する場合は準備する必要はありません。 一般的には、コマンドを 4 回以上実行する場合に準備します。  
  
 パフォーマンス上の理由から、コマンドの準備は、コマンドが実行されるまで遅延されます。 これは既定の動作です。 準備中のコマンドのエラーは、コマンドまたはメタプロパティ操作が実行されるまで認識されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SSPROP_DEFERPREPARE プロパティを FALSE に設定すると、この既定の動作を無効にできます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、コマンドを (最初に準備しないで) 直接実行すると、実行プランが作成され、キャッシュされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には新しいステートメントをキャッシュ内の既存の実行プランと照合する効率的なアルゴリズムがあるので、SQL ステートメントを再実行すると、そのステートメントの実行プランが再利用されます。  
  
 準備されたコマンドに対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではコマンド ステートメントの準備と実行に関するネイティブ サポートが提供されます。 ステートメントを準備すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では実行プランが作成されてキャッシュされ、この実行プランのハンドルがプロバイダーに返されます。 その後、プロバイダーはこのハンドルを使用して、ステートメントを繰り返し実行します。 ストアド プロシージャは作成されません。 直接実行する場合のように SQL ステートメントをキャッシュ内の実行プランと照合するのではなく、ハンドルで SQL ステートメントの実行プランを直接識別するので、そのステートメントを複数回実行することがわかっている場合は、ステートメントを準備する方が直接実行するよりも効率的です。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、準備されたステートメントを一時オブジェクトの作成に使用できません。また、準備されたステートメントから、一時テーブルなどの一時オブジェクトを作成するシステム ストアド プロシージャを参照できません。 このようなプロシージャは、直接実行する必要があります。  
  
 コマンドによっては、準備してはいけないものがあります。 たとえば、ストアド プロシージャの実行を指定するコマンドや、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャの作成に関して無効なテキストを含むコマンドは、準備しないようにしてください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、一時ストアド プロシージャが作成されると、その一時ストアド プロシージャを実行して、そのステートメント自体が実行されたかのように結果を返します。  
  
 一時ストアド プロシージャの作成は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー固有の初期化プロパティである SSPROP_INIT_USEPROCFORPREP によって制御されます。 プロパティ値が SSPROPVAL_USEPROCFORPREP_ON または SSPROPVAL_USEPROCFORPREP_ON_DROP の場合、コマンドが準備されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、ストアド プロシージャの作成を試みます。 ストアド プロシージャの作成は、アプリケーション ユーザーが適切な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 権限を所持している場合に成功します。  
  
 ほとんど切断しないコンシューマーの場合、一時ストアド プロシージャの作成には、**tempdb** の大量のリソースが必要になることがあります。tempdb は、一時オブジェクトが作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データベースです。 SSPROP_INIT_USEPROCFORPREP の値が SSPROPVAL_USEPROCFORPREP_ ON の場合、コマンドを作成したセッションで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続が失われたときにだけ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーで作成された一時ストアド プロシージャが削除されます。 その接続がデータ ソースの初期化時に作成された既定の接続の場合は、データ ソースの初期化が解除されたときのみ、一時ストアド プロシージャが削除されます。  
  
 SSPROP_INIT_USEPROCFORPREP の値が SSPROPVAL_USEPROCFORPREP_ON_DROP の場合、次のいずれかの時点で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの一時ストアド プロシージャが削除されます。  
  
-   コンシューマーが **ICommandText::SetCommandText** を使用して新しいコマンドを指定したとき。  
  
-   コンシューマーが **ICommandPrepare::Unprepare** を使用して、コマンド テキストが必要なくなったことを指定したとき。  
  
-   コンシューマーが一時ストアド プロシージャを使用して、コマンド オブジェクトへのすべての参照を解放したとき。  
  
 コマンド オブジェクトは、最大で 1 つだけ一時ストアド プロシージャを **tempdb** に保持します。 既存の一時ストアド プロシージャは、特定のコマンド オブジェクトに関する現在のコマンド テキストを表します。  
  
## <a name="see-also"></a>参照  
 [コマンド](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
