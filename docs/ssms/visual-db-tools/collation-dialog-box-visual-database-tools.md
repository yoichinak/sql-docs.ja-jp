---
description: '[照合順序] ダイアログ ボックス (Visual Database Tools)'
title: '[照合順序] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: c1e4c82b90c9b3c569f9f179ed16242c4ca76f40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88314658"
---
# <a name="collation-dialog-box-visual-database-tools"></a>[照合順序] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このダイアログ ボックスを使用すると、列の照合順序を指定できます。 列の照合順序は、列の値を別の列や定数値と比較する演算で使用されます。 また、SUBSTRING や CHARINDEX などの一部の文字列関数の動作にも影響します。 列の照合順序設定による影響の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のドキュメントを参照してください。  
  
このダイアログ ボックスは以下の場合に表示されます。  
  
-   **[列のプロパティ]** タブの **[照合順序]** フィールドに無効な照合順序名を入力した場合。  
  
-   **[列のプロパティ]** タブの **[照合順序]** フィールドをクリックし、フィールドの右の省略記号ボタン ( **[...]** ) をクリックした場合。  
  
## <a name="options"></a>オプション  
**[SQL 照合順序]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定義された照合順序をドロップダウン リストから選択します。  
  
**[Windows 照合順序]**  
Windows によって定義された照合順序をドロップダウン リストから選択します。  
  
**[バイナリ並べ替え]**  
比較用に文字の値のバイナリ コードを使用します。 このオプションを選択すると、特定のアルファベット比較オプションが使用できなくなります。 たとえば、アルファベットの大文字と小文字のバイナリ コードは異なるため、大文字と小文字を区別しない比較はできなくなります。 **[Windows 照合順序]** を選択した場合にだけ適用されます。  
  
**[辞書並べ替え]**  
アルファベット比較オプションを使用します。 **[Windows 照合順序]** を選択した場合にだけ適用されます。 次のアルファベット比較オプションを使用できます。  
  
-   **[大文字と小文字を区別する]** : 大文字と小文字を別の文字として扱う場合に選択します。  
  
-   **[アクセントを区別する]** : 文字にアクセント記号が付いている場合と付いていない場合をそれぞれ別の文字として扱うときに選択します。 このオプションを選択すると、別のアクセント記号が付いている場合にも別の文字として扱われます。  
  
-   **[カタカナを区別する]** : 日本語のひらがなとカタカナを区別して扱う場合に選択します。  
  
-   **[文字幅を区別する]** : 半角文字と全角文字を区別して扱う場合に選択します。  
  
**[既定値に戻す] ボタン**  
データベースの既定の照合順序を列に適用します。  
  
## <a name="see-also"></a>参照  
[集計クエリにおける列の使用 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
