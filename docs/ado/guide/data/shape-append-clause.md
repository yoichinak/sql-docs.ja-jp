---
description: Shape の APPEND 句
title: Shape APPEND 句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: rothja
ms.author: jroth
ms.openlocfilehash: 11d2c02d24753460f90452ddd6cc6b1e1589b80b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979623"
---
# <a name="shape-append-clause"></a>Shape の APPEND 句
Shape コマンド APPEND 句は、1つまたは複数の列を **レコードセット**に追加します。 多くの場合、これらの列は、子 **レコードセット**を参照するチャプター列です。  
  
## <a name="syntax"></a>構文  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>説明  
 この句の部分は次のとおりです。  
  
 *親-コマンド*  
 0または次のいずれかです ( *親コマンド* を完全に省略できます)。  
  
-   {}**レコードセット**オブジェクトを返す、中かっこ ("") で囲まれたプロバイダーコマンド。 コマンドは基になるデータプロバイダーに対して発行され、その構文はそのプロバイダーの要件によって異なります。 これは通常 SQL 言語ですが、ADO では特定のクエリ言語を必要としません。  
  
-   かっこで囲まれた別の shape コマンド。  
  
-   テーブルキーワードと、その後にデータプロバイダーのテーブル名を指定します。  
  
 *parent-alias*  
 親 **レコードセット**を参照する、省略可能なエイリアス。  
  
 *列一覧*  
 次の1つまたは複数を実行します。  
  
-   集計列。  
  
-   計算列。  
  
-   新しい句を使用して作成された新しい列。  
  
-   チャプター列。 チャプター列定義は、かっこ ("()") で囲まれています。 次の構文を参照してください。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>解説  
 *子レコードセット*  
 -   {}**レコードセット**オブジェクトを返す、中かっこ ("") で囲まれたプロバイダーコマンド。 コマンドは基になるデータプロバイダーに対して発行され、その構文はそのプロバイダーの要件によって異なります。 これは通常 SQL 言語ですが、ADO では特定のクエリ言語を必要としません。  
  
-   かっこで囲まれた別の shape コマンド。  
  
-   既存の形状が指定された **レコードセット**の名前。  
  
-   テーブルキーワードと、その後にデータプロバイダーのテーブル名を指定します。  
  
 *子-エイリアス*  
 子 **レコードセット**を参照する別名。  
  
 *親列*  
 *親コマンド*によって返される**レコードセット**内の列。  
  
 *子列*  
 *子コマンド*によって返される**レコードセット**内の列。  
  
 *param-数値*  
 「 [パラメーター化コマンドの操作」を](../../../ado/guide/data/operation-of-parameterized-commands.md)参照してください。  
  
 *章-エイリアス*  
 親に追加されたチャプター列を参照する別名。  
  
> [!NOTE]
>  *"親列*から*子列*への" 句は実際にはリストです。各リレーションシップは、コンマで区切られます。  
  
> [!NOTE]
>  APPEND キーワードの後の句は実際にはリストです。各句はコンマで区切り、親に追加する別の列を定義します。  
  
SHAPE コマンドの一部としてユーザー入力からプロバイダーコマンドを構築すると、SHAPE はユーザーが指定したプロバイダーコマンドを不透明な文字列として扱い、そのコマンドをプロバイダーに忠実に渡します。 たとえば、次の SHAPE コマンドでは、  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 図形は2つのコマンド `select * from t1` (と) を実行し `select * from t2 RELATE k1 TO k2)` ます。 ユーザーが複数のプロバイダーコマンドで構成される複合コマンドをセミコロンで区切って指定した場合、図形はその違いを区別できません。 したがって、次の SHAPE コマンドでは、  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 図形 `select * from t1; drop table t1` が実行され `select * from t2 RELATE k1 TO k2),` ます ( `drop table t1` これは独立したものであり、この場合は危険なプロバイダーコマンドです)。 アプリケーションは、このようなハッカー攻撃が発生するのを防ぐために、常にユーザー入力を検証する必要があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [非パラメーター化コマンドの操作](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [パラメーター化コマンドの操作](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [ハイブリッド コマンド](../../../ado/guide/data/hybrid-commands.md)  
  
-   [介在する Shape COMPUTE 句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [仮形の文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
