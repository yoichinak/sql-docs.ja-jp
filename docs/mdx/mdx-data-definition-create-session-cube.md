---
description: MDX データ操作 - CREATE SESSION CUBE
title: CREATE SESSION CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33cdbc4a018245249771ff350227d13f4e0f772e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483875"
---
# <a name="mdx-data-definition---create-session-cube"></a>MDX データ操作 - CREATE SESSION CUBE


  既存のサーバー キューブから、セッション キューブを作成および設定します。 セッション キューブは現在のセッション内でのみ表示できます。他のセッションから参照したり、クエリを実行することはできません。 セッション キューブは、セッションが閉じられたときに暗黙的に削除されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN  
  
```  
  
## <a name="syntax-elements"></a>構文要素  
 session_cube_name  
 セッション キューブの名前です。  
  
 source_cube_name  
 作成するセッション キューブの基になるキューブの名前です。  
  
 source_cube_name。 measure_name  
 セッションキューブに含まれる、基になるメジャーの完全修飾名です。 メジャーディメンションの計算されるメンバーは使用できません。  
  
 measure_name  
 セッション キューブのメジャーの名前です。  
  
 source_cube_name。 dimension_name  
 セッションキューブに含まれる、基になるディメンションの完全修飾名です。  
  
 dimension_name  
 セッションキューブ内のディメンションの名前です。  
  
 FROM \<dim from clause>  
 派生ディメンションの定義のみの有効な仕様です。  
  
 NOT_RELATED_TO_FACTS  
 派生ディメンションの定義のみの有効な仕様です。  
  
 \<level type>  
 派生ディメンションの定義のみの有効な仕様です。  
  
## <a name="remarks"></a>解説  
 サーバー キューブやローカル キューブと異なり、セッション キューブは、それを作成したセッションの期間を超えて保持されません。 セッションキューブは、それを定義するメジャーと定義に基づいて定義されます。 ディメンションには、次の2種類があります。  
  
-   ソースディメンション-これは、ソースキューブの1つに含まれていたディメンションです。  
  
-   派生ディメンション-新しい分析機能を提供するディメンションです。 派生ディメンションは、垂直方向または水平方向にスライスされるか、ディメンションメンバーのカスタムグループが含まれている、ソースディメンションに基づいて定義された標準のディメンションにすることができます。 また、派生ディメンションは、データ マイニング モデルに基づくデータ マイニング ディメンションである場合もあります。  
  
> [!NOTE]  
>  Dimension キーワードは、ディメンションまたは階層を参照できます。  
  
 セッションキューブは主に、Microsoft Excel などのクライアントアプリケーションによってカスタムメンバーグループに属性メンバーを動的にグループ化するために使用されます。 セッションキューブでは、次のタスクを実行できます。  
  
-   ソース キューブに存在するディメンションを削除する。  
  
-   ディメンションの階層を追加または削除します。  
  
-   メジャーグループまたは特定のメジャーを削除します。  
  
-   既存の属性に対してグループを作成するために、属性のバインドに基づいて新しい属性を追加します。  
  
> [!IMPORTANT]  
>  セッション キューブ オブジェクトのセキュリティは、基になるソース オブジェクトのセキュリティを継承します。 アクションや計算スクリプトなどの他のオブジェクトも、セッションキューブによって継承されます。  
  
 CREATE SESSION CUBE ステートメントは、次の規則に従います。  
  
-   親子階層ではグループ化を実行できません。  
  
-   ROLAP ディメンションでグループ化を実行することはできません。  
  
-   リンクディメンションでグループ化を実行することはできません。  
  
-   カスタムロールアップを持つレベルでグループ化を実行することはできません。  
  
-   分離された属性階層ではグループ化を実行できません。  
  
-   不自然な階層でグループ化を実行することはできません。これは、年齢や性別など、レベル間の多対多リレーションシップを持つ階層です。  
  
-   MDX スクリプト内でキューブ名を明示的に参照しても、セッション キューブでは名前が異なるためグループ化によって参照が無効になります。 代わりに CURRENTCUBE キーワードを使用してください。  
  
-   明示的な既定メンバーを持つディメンションではグループ化を実行できません。  
  
-   グループ化を実行すると、元のサーバーキューブのセッションスコープの計算されるメンバーは削除されます。  
  
-   サーバー キューブのキューブ ディメンションでグループ化を実行する場合、同じディメンションに基づくすべてのキューブ ディメンションに影響します。  
  
## <a name="example"></a>例  
 次の例では、再販業者の Sales Amount メジャー、再販業者のディメンション、Product ディメンション、Geography ディメンション、および Date ディメンションが含まれている、セッションスコープバージョンの Adventure Works キューブを作成する方法を示します。 このセッション キューブ内では 2 つのグループが作成されます。1 つはヨーロッパ諸国を含み、もう 1 つは北米の国々を含みます。 このサンプルは、ユーザーがメンバーのカスタムグループを作成するときに Microsoft Excel によって発行される CREATE SESSION CUBE ステートメントの簡略化されたバージョンです。  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)   
 [MDX&#41;&#40;のグローバルキューブステートメントの作成 ](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
