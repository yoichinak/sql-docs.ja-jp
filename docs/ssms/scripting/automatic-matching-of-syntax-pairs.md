---
title: 構文ペアの自動照合
description: クエリ エディター (区切り記号の照合)、XMLA クエリ エディター (中かっこの照合)、MDX と DMX (かっこの照合) での構文ペアの自動照合について学習します。
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bf089cd4cc48a04afd867a3e8b805eb9097e8c2
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902077"
---
# <a name="automatic-matching-of-syntax-pairs"></a>構文ペアの自動照合
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  構文ペアの自動照合では、ペアでコーディングする必要がある構文要素が正しくペアになっているかどうかをすぐに検出します。 この機能は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターでは区切り記号の照合、Analysis Services の XMLA クエリ エディターでは中かっこの照合、MDX エディターと DMX エディターではかっこの照合として知られています。  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>データベース エンジンのクエリ エディターでの区切り記号の照合  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターでは、コード ブロックの境界を識別する区切り記号が照合されます。 照合は、次の 2 とおりの方法で行われます。  
  
-   ペアの 2 番目の区切り記号の入力が終了すると、ペアになる両方の区切り記号が強調表示されます。  
  
-   ペアのいすれかの区切り記号にカーソルが置かれていれば、&lt;localizedText&gt;Ctrl&lt;/localizedText&gt; キーを押しながら &lt;localizedText&gt;]&lt;/localizedText&gt; キーを押すと、対応する区切り記号に移動できます。  
  
### <a name="delimiter-pairs"></a>区切り記号のペア  
 区切り記号の自動照合では、次の区切り記号のペアが認識されます。  
  
|開始区切り記号|終了区切り記号|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 区切り記号の自動照合では、角かっこで囲まれた識別子 ([ObjectName]) や引用符で囲まれた識別子 ("ObjectName") は認識されません。 ペアの照合では、文字列リテラル ('string') の単一引用符区切り記号は照合されません。文字列が区切られているかどうかが既に色分け表示されているためです。  
  
### <a name="delimiter-highlighting"></a>区切り記号の強調表示  
 照合により、区切り記号のペアの開始要素と終了要素がどちらも強調表示されます。 これにより、コード ブロックを視覚的に認識し、対応していない区切り記号のペアを確認できます。  
  
 最後の文字を入力してペアが完成すると、区切り記号が強調表示されます。 たとえば、BEGIN の後に END を入力する BEGIN END ペアの場合、END の最後の文字を入力すると区切り記号が強調表示されます。 必ずしも、開始区切り記号を入力した後に終了区切り記号を入力すると強調表示されるわけではありません。 最初に END を入力し、スクリプトを上にスクロールして、BEGIN を入力した場合、BEGIN の最後の文字を入力したときに区切り記号が強調表示されます。 最後に入力する文字は、区切り記号の最後の文字でなくてもかまいません。 たとえば、BEGIN のスペルを間違えて BEIN と入力した場合、最後に文字 G を挿入すると、BEGIN END のペアが強調表示されます。  
  
 区切り記号のペアは、カーソルを移動するまで強調表示されたままです。 新しいカーソル位置が同じ区切り記号の中にあっても、カーソルを移動すると強調表示が解除されます。 ペアのいずれかの任意の文字を削除してから再入力すると、再度強調表示することができます。  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Analysis Services の XMLA クエリ エディターでの中かっこの照合  
 XMLA クエリ エディターの中かっこの照合では、左中かっこと右中かっこが強調表示され、要素が閉じられたかどうかを示します。 また、<localizedText>Ctrl</localizedText> キーを押しながら <localizedText>]</localizedText> キーを押して、中かっこから対応する中かっこに移動することもできます。  
  
 XMLA クエリ エディターでは、次の用語に対して中かっこの照合が行われます。  
  
-   照合の開始タグと終了タグ。  
  
-   ペアの "\<" and ">" の山かっこ。  
  
-   コメントの開始と終了  
  
-   処理命令の開始と終了  
  
-   CDATA ブロックの開始と終了  
  
-   DTD 宣言の開始と終了  
  
-   属性の開始と終了の引用符  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>MDX エディターと DMX エディターでのかっこの照合  
 多次元式 (MDX) エディターとデータ マイニング式 (DMX) のエディターでは、関数のかっこのペアが自動的に照合されます。
