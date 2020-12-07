---
title: パラメーター ヒント (IntelliSense)
description: IntelliSense のパラメーター ヒント オプションを使用する方法について説明します。これにより、関数やストアド プロシージャに必要なパラメーターについて入力すると情報が提供されます。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 806d153589f05f8e2a945f7c8e1e34b1aab57aab
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036445"
---
# <a name="parameter-info-intellisense"></a>パラメーター ヒント (IntelliSense)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense の **[パラメーター ヒント]** オプションを使用すると、パラメーター リストが表示され、関数またはストアド プロシージャで必要とされるパラメーターの数、名前、およびデータ型について確認できます。 太字で表示されるパラメーターは、入力中の関数やストアド プロシージャで次に必要なパラメーターを示しています。  
  
 パラメーター リストは入れ子にされた関数についても表示されます。 他の関数のパラメーターとして関数を入力する場合、パラメーター リストには内部関数のパラメーターが表示されます。 内部関数のパラメーター リストが完了すると、パラメーター リストには再び外部関数のパラメーターが表示されます。  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>関数またはストアド プロシージャのパラメーター ヒントを表示するには  
  
1.  関数の場合、名前の後に、通常と同じように左かっこを入力すると、パラメーター リストが表示されます。 ストアド プロシージャの場合、名前を入力した後に、通常と同じようにスペースを入力すると、プロシージャのパラメーターに関する情報が表示されます。  
  
     IntelliSense は、関数の宣言全体またはストアド プロシージャのパラメーターをポップアップ ウィンドウとして挿入ポイントのすぐ下に表示します。 リスト内の最初のパラメーターは太字で表示されます。  
  
2.  パラメーターを入力していくと、次に入力する必要のあるパラメーターに応じて太字が変わります。  
  
3.  Esc キーを押してリストを閉じるか、関数が完了するまで入力を続けます。  
  
     関数の場合、右かっこを入力するとパラメーター リストも閉じます。  
  
#### <a name="to-manually-start-parameter-info"></a>パラメーター ヒントを手動で起動するには  
  
1.  **[編集]** メニューの **[IntelliSense]** をポイントし、 **[パラメーター ヒント]** をクリックします。  
  
2.  Ctrl&lt;/localizedText&gt; キーと &lt;localizedText&gt;Shift&lt;/localizedText&gt; キーを押しながら &lt;localizedText&gt;Space&lt;/localizedText&gt; キーを押します。  
  
 詳細については、「[IntelliSense の構成 &#40;SQL Server Management Studio&#41;](./configure-intellisense-sql-server-management-studio.md)」を参照してください。  
  
> [!NOTE]  
>  **[パラメーター ヒント]** オプションは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターと XML クエリ エディターでのみ使用できます。  
  
