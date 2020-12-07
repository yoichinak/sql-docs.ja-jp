---
description: MDX データ操作 - CREATE ACTION
title: CREATE ACTION ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7132c28e93dbc11eee1c5a4e4d53126f280fa74a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494905"
---
# <a name="mdx-data-definition---create-action"></a>MDX データ操作 - CREATE ACTION


  キューブ、ディメンション、階層、または下位のオブジェクトに関連付けることができるアクションを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列です。  
  
 *Action_ 名*  
 作成するアクションの名前を指定する有効な文字列です。  
  
 *Hierarchy_ 名*  
 階層名を提供する有効な文字列です。  
  
 *Level_ 名*  
 レベル名を提供する有効な文字列です。  
  
 *Member_ 名*  
 メンバー名またはメンバーキーを提供する有効な文字列。  
  
 *MDX_Expression*  
 有効な MDX 式です。  
  
 *String_Expression*  
 有効な文字列式。  
  
## <a name="remarks"></a>解説  
 クライアントアプリケーションは、安全でないアクションを作成および実行することができます。クライアントアプリケーションでは、unsafe 関数を使用することもできます。 このような状況を回避するには、[ **安全性オプション** ] プロパティを使用します。 詳細については、「Safety Options プロパティ」を参照してください。  
  
> [!NOTE]  
>  このステートメントは、旧バージョンとの互換性のために用意されています。 の新しいアクション ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ドリルスルーやレポートアクションなど) はサポートされていません。  
  
## <a name="action-types"></a>アクションの種類  
 次の表では、で使用できるさまざまな種類のアクションについて説明し [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。  
  
|アクションの種類|説明|  
|-----------------|-----------------|  
|**URL**|返されるアクション文字列は、インターネット ブラウザーで開く URL です。<br /><br /> 注: このアクションがまたはで始まっていない場合 `https://` `https://` 、[ **Saf etyoptions]** が **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**に設定されていない限り、この操作はブラウザーでは使用できません。|  
|**HTML**|返されるアクション文字列は HTML スクリプトです。 文字列をファイルに保存し、ファイルをインターネットブラウザーを使用して表示する必要があります。 この場合、生成された HTML の一部としてスクリプト全体が実行される可能性があります。|  
|**諸表**|返されるアクション文字列は、コマンドオブジェクトの **icommand:: SetText** メソッドを文字列に設定し、 **Icommand:: Execute**メソッドを呼び出すことによって実行する必要があるステートメントです。 コマンドが成功しなかった場合は、エラーが返されます。|  
|**セット**|返されるアクション文字列は、コマンドオブジェクトの **icommand:: SetText** メソッドを文字列に設定し、 **Icommand:: Execute** メソッドを呼び出すことによって実行する必要がある MDX ステートメントです。 要求されたインターフェイス ID (IID) は **Idataset**である必要があります。 データセットが作成されている場合、コマンドは成功します。 クライアント アプリケーションでは、返されたデータセットをユーザーが表示できるようにする必要があります。|  
|**セット**|**データセット**に似ていますが、 **IDATASET**の iid を要求するのではなく、クライアントアプリケーションは**IRowset**の iid を要求する必要があります。 行セットが作成されれば、コマンドは成功したことになります。 クライアントアプリケーションでは、返された行セットをユーザーが参照できるようにする必要があります。|  
|**DS**|クライアント アプリケーションでアクション文字列を実行します。 文字列はコマンドラインです。|  
|**各社**|アプリケーションに特定のアクションに関するカスタムの非ジェネリックナレッジがある場合を除き、クライアントアプリケーションでは、アクションを表示したり、実行したりしないでください。 クライアントアプリケーションが **APPLICATION_NAME**に適切な制限を設定することによって明示的に要求しない限り、独自のアクションはクライアントアプリケーションに返されません。|  
  
## <a name="invocation-types"></a>呼び出しの種類  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用できる呼び出しの種類は以下のとおりです。 呼び出しの種類は、クライアントアプリケーションによってのみ使用され、アクションを呼び出すタイミングを判断するのに役立ちます。 呼び出しの種類は、実際にはアクションの呼び出し動作を決定しません。  
  
|呼び出しの種類|説明|  
|---------------------|-----------------|  
|**静的**|アクションは、ユーザーの操作によってクライアントアプリケーションによって呼び出される必要があります。|  
|**ON_OPEN**|アクションは、ターゲットオブジェクトを開いたときに、クライアントアプリケーションによって呼び出される必要があります。 この呼び出しの種類は現在実装されていません。|  
|**バッチ**|クライアント アプリケーションは、対象のオブジェクトがバッチ操作にかかわった時点を判別してアクションを呼び出します。 この呼び出しの種類は現在実装されていません。|  
  
### <a name="scope"></a>スコープ  
 各アクションは、特定のキューブに対して定義され、そのキューブ内に一意の名前が付いています。 アクションは、次の表に示すいずれかのスコープを持つことができます。  
  
 キューブ スコープ  
 特定のディメンション、メンバー、セルに限定されないアクションです。たとえば、"AS/400 実稼働システムの端末エミュレーションの起動" などは、これに相当します。  
  
 ディメンションのスコープ  
 アクションは、特定のディメンションに適用されます。 この種のアクションは、選択された特定のレベルまたはメンバーに依存しません。  
  
 レベルのスコープ  
 特定のディメンション レベルに適用されるアクションです。 これらのアクションは、そのディメンション内のメンバーの特定の選択に依存しません。  
  
 メンバー スコープ  
 アクションは、特定のレベルメンバーに適用されます。  
  
 セル スコープ  
 特定のセルだけに適用されるアクションです。  
  
 セット スコープ  
 アクションは、セットのみに適用されます。 名前 **ActionParameterSet**は、アクションの式の中でアプリケーションが使用するために予約されています。  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
