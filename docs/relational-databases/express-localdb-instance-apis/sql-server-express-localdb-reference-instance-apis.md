---
description: SQL Server Express LocalDB リファレンス - インスタンス API
title: SQL Server Express LocalDB インスタンスの API リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 892ccbc66070e7ef0d198daba60698502ee3bd0f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541195"
---
# <a name="sql-server-express-localdb-reference---instance-apis"></a>SQL Server Express LocalDB リファレンス - インスタンス API
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  従来のサービスベースの SQL Server 環境で、単一のコンピューターにインストールされた個々の SQL Server インスタンスは、物理的に独立しています。つまり、各インスタンスは独立したバイナリ セットを持っており、独立したサービス プロセスの下で実行されます。インストールと削除も個別に行われる必要があります。 ユーザーが接続する先の SQL Server インスタンスは、SQL Server インスタンス名を使用して指定されます。  
  
 SQL Server Express LocalDB インスタンス API は、簡略化された "軽量な" インスタンスモデルを使用します。 個々の LocalDB インスタンスは、ディスク上とレジストリ内で独立していますが、同じ 1 組の共有 LocalDB バイナリを使用します。 また、LocalDB ではサービスが使用されません。LocalDB インスタンスは、LocalDB インスタンス API 呼び出しを介して要求時に起動されます。 LocalDB では、ユーザーが使用する LocalDB インスタンスを指定するために、インスタンス名が使用されます。  
  
 LocalDB インスタンスは、常に1人のユーザーによって所有され、インスタンス共有が有効になっている場合を除き、このユーザーのコンテキストからのみアクセスできます。  
  
 厳密には、LocalDB インスタンスは従来の SQL Server インスタンスとは異なりますが、意図されている用途はほぼ同じです。 これらは *インスタンス* と呼ばれ、この類似性を強調し、SQL Server ユーザーにとって直観的にするために使用されます。  
  
 LocalDB では、自動インスタンス (AI) と名前付きインスタンス (NI) という 2 種類のインスタンスがサポートされています。 LocalDB インスタンスの識別子は、インスタンス名です。  
  
## <a name="automatic-localdb-instances"></a>自動 LocalDB インスタンス  
 自動 LocalDB インスタンスは "パブリック" です。ユーザーに対して自動的に作成および管理され、任意のアプリケーションで使用できます。 ユーザーのコンピューターにインストールされている LocalDB のバージョンごとに、1つの自動 LocalDB インスタンスが存在します。  
  
 自動 LocalDB インスタンスを使用すると、シームレスなインスタンス管理を実行できます。 ユーザーがインスタンスを作成する必要はありません。 これにより、ユーザーはアプリケーションのインストールや、複数の異なるコンピューターへの移行を容易に行うことができます。 ターゲット コンピューターに指定バージョンの LocalDB がインストールされている場合、そのコンピューターでは、同じバージョンの自動 LocalDB インスタンスも使用できます。  
  
### <a name="automatic-instance-management"></a>自動インスタンス管理  
 ユーザーは、自動 LocalDB インスタンスを作成する必要はありません。 指定されたバージョンの LocalDB がユーザーのコンピューターで使用可能な場合は、インスタンスの初回使用時にインスタンスが遅延作成されます。 ユーザーの視点から見ると、LocalDB バイナリが存在する場合、自動インスタンスは常に存在します。  
  
 自動インスタンスには、削除、共有、共有解除など、その他のインスタンス管理操作も使用できます。 特に、自動インスタンスを削除すると、そのインスタンスが効果的にリセットされ、次回の起動操作時に再作成されます。 システム データベースが破損した場合は、自動インスタンスの削除が必要になる場合があります。  
  
### <a name="automatic-instance-naming-rules"></a>自動インスタンスの名前付け規則  
 自動 LocalDB インスタンスのインスタンス名には特殊なパターンがあり、これは予約済み名前空間に属します。 このようなパターンが必要になるのは、名前付き LocalDB インスタンスと名前が競合するのを防ぐためです。  
  
 自動インスタンス名は、LocalDB のベースラインリリースバージョン番号で、前に1つの "v" 文字が付いています。 これは "v" のように、2つの数値の間にピリオドを加えたものです。たとえば、「v 11.0」や「-12.00」のようにします。  
  
 無効な自動インスタンス名の例を次に示します。  
  
-   11.0 (先頭に "v" 文字がありません)  
  
-   v11 (ピリオドと 2 番目のバージョン番号がありません)  
  
-   v11. (2 番目のバージョン番号がありません)  
  
-   v11.0.1.2 (バージョン番号の数が 2 つを超えています)  
  
## <a name="named-localdb-instances"></a>名前付き LocalDB インスタンス  
 名前付き LocalDB インスタンスは "プライベート" です。インスタンスは、インスタンスの作成と管理を担当する1つのアプリケーションによって所有されます。 名前付き LocalDB インスタンスを使用すると、そのインスタンスを分離することで、パフォーマンスの向上を図ることができます。  
  
### <a name="named-instance-creation"></a>名前付きインスタンスの作成  
 名前付きインスタンスは、ユーザーが LocalDB 管理 API を通じて明示的に作成するか、マネージド アプリケーションの app.config ファイルを通じて暗黙的に作成する必要があります。 この API は、マネージド アプリケーションでも使用できます。  
  
 各名前付きインスタンスには、特定の LocalDB バージョンが関連付けらています。つまり、各名前付きインスタンスは、LocalDB バイナリの特定のセットを指しています。 名前付きインスタンスのバージョンは、インスタンス作成時に設定されます。  
  
### <a name="named-instance-naming-rules"></a>名前付きインスタンスの名前付け規則  
 LocalDB インスタンス名の最大文字数は128文字です ( **sysname** データ型によって制限されています)。 これは、従来の SQL Server インスタンス名と比較すると、大きく異なります。従来は、16 の ASCII 文字で構成される NetBIOS 名に制限されていました。 この違いの理由は、LocalDB ではデータベースがファイルとして扱われるため、ファイルベースのセマンティクスを意味するので、ユーザーはより自由にインスタンス名を選択できます。  
  
 LocalDB のインスタンス名には、ファイル名コンポーネント内で有効な任意の Unicode 文字を使用できます。 ファイル名コンポーネント内の無効な文字には、通常、ASCII/Unicode 文字 1 ~ 31 の文字、引用符 (")、小なり ( \<), greater than (> )、パイプ (|)、バックスペース (\b)、タブ (\t)、コロン (:)、アスタリスク (*)、疑問符 (?)、円記号 ( \\ )、およびスラッシュ (/) が含まれます。 null 文字 (\0) は、文字列の終端として許可されています。最初に検出された null 文字以降は、すべての文字が無視されます。  
  
> [!NOTE]  
>  無効な文字はオペレーティング システムによって異なり、今後のリリースで変わることもあります。  
  
 インスタンス名の先頭と末尾の空白は無視され、トリミングされます。  
  
 名前の競合を回避するには、「自動インスタンスの名前付け規則」で既に説明したように、名前付き LocalDB インスタンスには自動インスタンスの名前付けパターンに従った名前を付けることはできません。 自動インスタンスの名前付けパターンに従った名前の名前付きインスタンスを作成しようとすると、既定のインスタンスが実質的に作成されます。  
  
## <a name="sql-server-express-localdb-reference-topics"></a>SQL Server Express LocalDB リファレンス トピック  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
 LocalDB インスタンス API を見つけるためのヘッダー ファイル情報とレジストリ キーを提供します。  
  
 [コマンドライン管理ツール:SqlLocalDB.exe](../../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
 コマンド ラインから LocalDB インスタンスを管理するツールである SqlLocalDB.exe について説明します。  
  
 [LocalDBCreateInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbcreateinstance-function.md)  
 LocalDB インスタンスを新規作成するための関数について説明します。  
  
 [LocalDBDeleteInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbdeleteinstance-function.md)  
 LocalDB インスタンスを削除する関数について説明します。  
  
 [LocalDBFormatMessage 関数](../../relational-databases/express-localdb-instance-apis/localdbformatmessage-function.md)  
 LocalDB エラーのローカライズされた説明を返す関数について説明します。  
  
 [LocalDBGetInstanceInfo 関数](../../relational-databases/express-localdb-instance-apis/localdbgetinstanceinfo-function.md)  
 LocalDB インスタンスの情報 (バージョン情報、存在するかどうか、実行中かどうかなど) を取得する関数について説明します。  
  
 [LocalDBGetInstances 関数](../../relational-databases/express-localdb-instance-apis/localdbgetinstances-function.md)  
 指定されたバージョンの LocalDB インスタンスをすべて返す関数について説明します。  
  
 [LocalDBGetVersionInfo 関数](../../relational-databases/express-localdb-instance-apis/localdbgetversioninfo-function.md)  
 指定された LocalDB バージョンの情報を返す関数について説明します。  
  
 [LocalDBGetVersions 関数](../../relational-databases/express-localdb-instance-apis/localdbgetversions-function.md)  
 コンピューターにインストールされているすべての LocalDB バージョンを返す関数について説明します。  
  
 [LocalDBShareInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbshareinstance-function.md)  
 指定された LocalDB インスタンスを共有するための関数について説明します。  
  
 [LocalDBStartInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbstartinstance-function.md)  
 指定された LocalDB インスタンスを起動する関数について説明します。  
  
 [LocalDBStartTracing 関数](../../relational-databases/express-localdb-instance-apis/localdbstarttracing-function.md)  
 ユーザーの API トレースを有効にする関数について説明します。  
  
 [LocalDBStopInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbstopinstance-function.md)  
 指定された LocalDB インスタンスの実行を停止する関数について説明します。  
  
 [LocalDBStopTracing 関数](../../relational-databases/express-localdb-instance-apis/localdbstoptracing-function.md)  
 ユーザーの API トレースを無効にする関数について説明します。  
  
 [LocalDBUnshareInstance 関数](../../relational-databases/express-localdb-instance-apis/localdbunshareinstance-function.md)  
 指定された LocalDB インスタンスの共有を停止する関数について説明します。  
  
  
