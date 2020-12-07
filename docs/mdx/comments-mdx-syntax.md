---
description: コメント (MDX 構文)
title: コメント (MDX 構文) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa1312e361bf0ef673254c0eb804ed7b8b7ca7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387677"
---
# <a name="comments-mdx-syntax"></a>コメント (MDX 構文)


  コメントは、プログラムコード内の実行されていないテキスト文字列です。 (コメントは "注釈" とも呼ばれます)。 コメントを使用してコードを文書化したり、診断対象の多次元式 (MDX) ステートメントおよびスクリプトの一部を一時的に無効にしたりすることができます。 コメントを使用してコードを記述することで、将来のプログラムコードの保守を容易にすることができます。 また、プログラム名、作成者名、およびコードの主要な変更日を記録するためにコメントを使用する場合も少なくありません。 また、コメントを使用して複雑な計算を記述したり、プログラミング方法を説明したりすることもできます。  
  
 MDX のコメントは、次のガイドラインに従います。  
  
-   コメント内では、すべての英数字または記号を使用できます。  コメント内のすべての文字は無視されます。  
  
-   ステートメント内またはスクリプト内のコメント長には制限がありません。 1つまたは複数の行からコメントを作成できます。  
  
 MDX では、次の3種類のコメント文字がサポートされています。  
  
 // (二重スラッシュ)  
 これらのコメント文字は、実行するコードと同じ行に記述することも、単独で使用することもできます。 二重スラッシュから行末までのすべてがコメントの一部となります。 複数行のコメントの場合は、各コメント行の先頭に二重スラッシュが表示されます。 詳細については、「 [ MDX&#41;&#41; &#40;コメントを&#40;](../mdx/comment-mdx-double-slash.md)」を参照してください。  
  
 -- (二重ハイフン)  
 これらのコメント文字は、実行するコードと同じ行に記述することも、単独で使用することもできます。 二重ハイフンから行末までのすべてがコメントの一部になります。 複数行にわたってコメントを記述する場合、それぞれのコメント行の先頭に二重ハイフンを入力する必要があります。 詳細については、「 [MDX&#41;&#41; &#40;コメントを &#40;](../mdx/comment-mdx-operator-reference.md)」を参照してください。  
  
 /* ... \*/(スラッシュとアスタリスクの文字のペア)  
 このコメント文字では、実行コードと同じ行にコメントを記述できるほか、コメント専用の行にすることもできます。さらに、実行可能コード内でもこのコメント文字を使用できます。 開いているコメントのペア (/ \* ) から終了コメントのペア (/) までのすべての要素 \* は、コメントの一部と見なされます。 複数行のコメントの場合、コメントの先頭にコメントを入れる必要があります。また、コメントの終わりにコメントを入れる必要があり \* \* ます。 コメントの行に他のコメント文字を含めることはできません。 詳細については、「 [/*... \* 」を参照してください。/(コメント)](../mdx/comment-mdx.md)。  
  
## <a name="example"></a>例  
 次のクエリは、3種類のコメントすべての例を示しています。  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 構文の要素 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
