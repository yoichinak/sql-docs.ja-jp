---
title: SQLXML のセキュリティに関する主な注意点
description: データアクセスに SQLXML を使用する場合の主要なセキュリティガイドラインについて説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9841e46f97248413f142886193d9c2afedbe4e04
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809799"
---
# <a name="core-sqlxml-security-considerations"></a>SQLXML のセキュリティに関する主な注意点
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  次に、データ アクセスに SQLXML を使用するときのセキュリティ ガイドラインを示します。  
  
-   SQLXMLOLEDB プロバイダーは **streamflags** プロパティを公開します。このプロパティを使用すると、特定のインスタンスごとに有効または無効にする SQLXML 機能を示すフラグを設定できます。 このプロパティを使用して、必要なコンポーネントだけが有効になるよう、SQLXML の使用をカスタマイズすることをお勧めします。 詳細については、「 [SQLXMLOLEDB Provider &#40;SQLXML 4.0&#41;](../data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)」を参照してください。  
  
-   SQLXML エラーが発生した場合、返されるメッセージには、テーブル名、列名、種類の情報など、データベース スキーマに関する情報を含めることができます。 これらのエラーを扱うときには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールに関する情報が関係のないユーザーに伝わらないよう注意する必要があります。  
  
-   SQLXML では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にクエリを実行したり更新を送信するにあたって、交換できるデータ量に制限は設定されません。また、処理前に SQLXML ペイロード内のデータのサイズに関してチェックは行われません。 SQLXML を使用してアプリケーションを開発する場合は、自身の責任で、システムにデータを処理する十分なメモリがあることを確認してください。 たとえば、サーバーに対してデータのクエリを実行するときには、クライアント側に、データを受信するだけの十分なメモリの空きがあることを確認する必要があります。 同様に、データをサーバーに読み込むときには、サーバー側に、データ処理に使用できるメモリと、データ保存に使用できるディスク保存領域が十分にあることを確認する必要があります。  
  
-   SQLXML では、動的に [!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリと更新コマンドが生成され、実行のため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。 これは、SQLXML がサーバーにクエリを実行して更新を適用する唯一の方法です。 結果は、(XML の) ストリームまたは行セットとして受信されます。  
  
-   SQLXML では、クエリ結果を受信しても、そのデータの内容に基づいて何らかの動作が行われるわけではありません。 データの種類や内容に基づいて追加処理は行われず、 操作を実行するためのコードとしてデータが使用されることはありません。  
  
-   XML テンプレートを実行すると、SQLXML では送信されたテンプレート内に含まれる XPath クエリと DBObject クエリが [!INCLUDE[tsql](../../../includes/tsql-md.md)] コマンドに変換され、そのコマンドが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対して実行されます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースの構造は変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの **sql: query** ブロックに含めることができます。  
  
-   DBObject クエリと XPath ステートメントをマッピング ファイルに対して実行しても、SQLXML でデータベース内のデータは一切変更されません。  
  
-   SQLXML では、XML と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ モデルの違いに基づき、指定されたデータの形式が変更される場合があります。 たとえば、時間を指定する形式はこれら 2 つで異なるため、 SQLXML ではこの違いの解決が試みられます。 この結果、一部の精度情報が失われる場合があります。  
  
-   SQLXML では、データ処理は時間の制限なく、 エラーが発生するか処理が完了するまで続けられます。  
  
-   SQLXML ではファイル システムへの書き込みは行われません。 データベースから取得したデータを保存するには、ユーザーが自分でコードを作成する必要があります。  
  
-   SQLXML では、ユーザーはデータベースに対して任意の SQL クエリを実行できます。 この場合、ユーザーの設定なしで SQL データベースを公開することになるため、保護または制御されていないソースに対してこの機能は提供しないでください。  
  
-   アップデートグラムを実行すると、SQLXML によって **updg: sync** ブロックがインスタンスに対する DELETE、UPDATE、および INSERT コマンドに変換され [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースは変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの **sql: query** ブロックに含めることができます。  
  
-   DiffGrams を実行すると、SQLXML では DiffGram が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに対する DELETE、UPDATE、および INSERT コマンドに変換されます。 これらのコマンドは、既存のデータにのみ影響します。 SQLXML により生成されるコマンドでは、データベースは変更されません。 データベースの構造を変更するには、ユーザーは明示的なコマンドを発行する必要があります。 たとえば、テンプレートの **sql: query** ブロックに含めることができます。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 のセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
  
