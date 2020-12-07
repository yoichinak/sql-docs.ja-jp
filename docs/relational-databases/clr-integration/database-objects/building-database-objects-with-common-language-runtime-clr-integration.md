---
title: 共通言語ランタイム (CLR) ビルドデータベースオブジェクト
description: .NET Framework 共通言語ランタイム (CLR) との SQL Server 統合を使用してデータベースオブジェクトを構築します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
ms.openlocfilehash: a891da3459e82bbb8c218fd68693840f141da93f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810846"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>CLR (共通言語ランタイム) 統合によるデータベース オブジェクトの構築
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と .NET Framework CLR (共通言語ランタイム) との統合を使用してデータベース オブジェクトを構築できます。 内で実行されるマネージコード [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、"CLR ルーチン" と呼ばれます。 CLR ルーチンには、次のものがあります。  
  
-   スカラー UDF (ユーザー定義スカラー値関数)  
  
-   ユーザー定義 TVF (テーブル値関数)  
  
-   UDP (ユーザー定義プロシージャ)  
  
-   ユーザー定義トリガー  
  
 CLR ルーチンは、マネージド コード内ではそれぞれ同じ構造になります。 CLR ルーチンは、クラスの public static ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET では shared) メソッドにマップされます。 ルーチン以外に、.NET Framework を使用して UDT (ユーザー定義型) やユーザー定義集計関数を定義することもできます。 UDT とユーザー定義集計は、.NET Framework クラス全体にマップされます。  
  
 各種類の .NET Framework ルーチンには [!INCLUDE[tsql](../../../includes/tsql-md.md)] 宣言があり、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で同等の [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用できる任意の場所で使用できます。 たとえば、スカラー UDF は任意のスカラー式で使用できます。 また、TVF は任意の FROM 句で使用できます。 プロシージャは、EXEC ステートメントやクライアント アプリケーションから呼び出すことができます。  
  
> [!NOTE]  
>  効果的であるとクエリ オプティマイザーで判断された場合は、共通言語ランタイムでの CLR オブジェクト (ユーザー定義関数、ユーザー定義型、またはトリガー) の実行を複数のスレッドで行うことができます (並列プラン)。 ただし、ユーザー定義関数がデータにアクセスする場合は、直列プランで実行されます。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] よりも前のサーバー バージョンで実行したときに、ユーザー定義関数に LOB パラメーターが含まれていたり、ユーザー定義関数から値が返される場合も、直列プランで実行する必要があります。  
  
 次の表に、このセクションで説明するトピックの一覧を示します。  
  
 [CLR 統合の概要](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR との統合を使用したオブジェクトのコンパイルに必要なライブラリと名前空間の概要について説明します。 また、例として "Hello World" CLR ストアド プロシージャを紹介します。  
  
 [サポートされている .NET Framework ライブラリ](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 CLR 統合でサポートされる .NET Framework ライブラリに関する情報を提供します。  
  
 [CLR 統合プログラミング モデルの制限事項](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 CLR 統合プログラミング モデルの制限事項に関する情報を提供します。  
  
 [.NET Framework での SQL Server データ型](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型と、.NET Framework での同等のデータ型の概要について説明します。  
  
 [CLR 統合のカスタム属性の概要](./clr-integration-custom-attributes-for-clr-routines.md)  
 CLR 統合のカスタム属性に関する情報を提供します。  
  
 [CLR ユーザー定義関数](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 テーブル値関数、スカラー関数、ユーザー定義集計関数など、さまざまな種類の CLR 関数の実装方法と使用方法について説明します。  
  
 [CLR ユーザー定義型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 CLR のユーザー定義型を実装して使用する方法について説明します。  
  
 [CLR ストアド プロシージャ](/dotnet/framework/data/adonet/sql/clr-stored-procedures)  
 CLR のストアド プロシージャを実装して使用する方法について説明します。  
  
 [CLR トリガー](/dotnet/framework/data/adonet/sql/clr-triggers)  
 CLR のトリガーを実装して使用する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [CLR&#41; 統合の概要 &#40;共通言語ランタイム](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
