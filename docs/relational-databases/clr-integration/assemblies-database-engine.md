---
title: アセンブリ (データベースエンジン) |Microsoft Docs
description: SQL Server インスタンスは、CLR 言語で記述された関数、プロシージャ、トリガー、ユーザー定義集計、および型を配置するアセンブリをホストできます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
ms.openlocfilehash: c3a507f250dcecf62560284916d543ca2f6d53c0
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810238"
---
# <a name="assemblies-database-engine"></a>アセンブリ (データベース エンジン)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このセクションのトピックでは、アセンブリの理解、設計、および実装に役立つ情報について説明します。  
  
 アセンブリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数、ストアドプロシージャ、トリガー、ユーザー定義集計、およびユーザー定義型を配置するために、のインスタンスで使用される DLL ファイルです [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。ではなく、共通言語ランタイム (CLR) によってホストされるマネージコード言語のいずれかで記述され [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイムで作成されたマネージド アプリケーション モジュール (.dll ファイル) を参照するオブジェクトです。 アセンブリには、クラス メタデータとマネージド コードが含まれています。 SQL Server のインスタンスにアセンブリをアップロードすることが、次のいずれかのデータベース オブジェクトを作成するための最初の手順になります。  
  
-   CLR 関数。 詳細については、「 [CLR 関数の作成](../../relational-databases/user-defined-functions/create-clr-functions.md)」を参照してください。  
  
-   CLR ストアド プロシージャ。 詳細については、「 [CLR ストアドプロシージャ](/dotnet/framework/data/adonet/sql/clr-stored-procedures)」を参照してください。  
  
-   CLR トリガー。 詳細については、「[CLR トリガーの作成](../../relational-databases/triggers/create-clr-triggers.md)」を参照してください。  
  
-   ユーザー定義集計関数。 詳細については、「 [ユーザー定義集計を作成する](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)」を参照してください。  
  
-   ユーザー定義型。 詳細については、「[ユーザー定義型の使用](../../relational-databases/native-client/features/using-user-defined-types.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、アセンブリによって次の関数が実行されます。  
  
-   上記の 1 つ以上の CLR データベース オブジェクトの機能を実行するマネージド コードを含む関数。  
  
-   アセンブリのバージョン番号とカルチャ、アセンブリのクラスの一覧を一意に識別する省略可能なパブリック キー、アセンブリで定義されたメソッド、アセンブリのプロセッサ アーキテクチャなどのメタデータを含む関数。  
  
-   コード アクセス権を管理することにより、マネージド コードがリソース外部にアクセスできる程度を管理する関数。  
  
-   アセンブリによって参照される他のアセンブリの依存関係に関するメタデータを含む関数。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)|アセンブリを作成する前の注意事項について説明します。 これには、アセンブリのパッケージ化、コード アクセス権、その他の制限事項などがあります。|  
|[アセンブリの実装](../../relational-databases/clr-integration/assemblies-implementing.md)|アセンブリを作成または削除する方法、アセンブリを変更するタイミングとその方法、およびアセンブリに関するメタデータの取得方法について説明します。|  
|[アセンブリについての情報の取得](../../relational-databases/clr-integration/assemblies-getting-information.md)|アセンブリに関するメタデータに対してクエリを実行可能なカタログ ビューや関数を一覧します。|  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
