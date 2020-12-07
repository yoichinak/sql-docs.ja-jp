---
description: 一般的な Shape コマンド
title: General | の Shape コマンドMicrosoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: rothja
ms.author: jroth
ms.openlocfilehash: c20132fe933d232d38ee843a706e9ad923d0d376
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724933"
---
# <a name="shape-commands-in-general"></a>一般的な Shape コマンド
データシェイプは、整形された **レコードセット**の列、列で表されるエンティティ間のリレーションシップ、および **レコードセット** にデータを設定する方法を定義します。  
  
 形状がある **レコードセット** は、次の種類の列で構成されます。  
  
|列の型|説明|  
|-----------------|-----------------|  
|[データ]|クエリコマンドによって返された **レコードセット** のフィールドを、データプロバイダー、テーブル、または以前に整形された **レコードセット**に返します。|  
|チャプター|*チャプター*と呼ばれる別の**レコードセット**への参照。 チャプター列を使用すると、親と *子* のリレーションシップを定義できます。 *親* は、チャプター列を含む **レコードセット** であり、 *子* はチャプターによって表される **レコードセット** です。|  
|集計 (aggregate)|列の値は、すべての行に対して *集計関数* を実行するか、子 **レコードセット**のすべての行の列に対して実行することによって得られます。 (次のトピックの「集計関数」、「集計関数」、「 [CALC 関数」、および「NEW キーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)」を参照してください)。|  
|計算式|列の値は、 **レコードセット**の同じ行の列に対して Visual Basic for Applications 式を計算することによって得られます。 式は、CALC 関数の引数です。 (次のトピックの「計算式」、「集計関数」、「CALC 関数」、「 [NEW キーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) 」、および「 [Visual Basic for Applications 関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)」を参照してください)。|  
|new|空の作成済みフィールド。後でデータを設定できます。 この列は、NEW キーワードで定義されています。 (次のトピックの「NEW キーワード」、「集計関数」、「 [CALC 関数」、および「New キーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)」を参照してください)。|  
  
 Shape コマンドには、 **レコードセット** オブジェクトを返す基になるデータプロバイダーに対してクエリコマンドを指定する句を含めることができます。 クエリの構文は、基になるデータプロバイダーの要件によって異なります。 これは通常 SQL ですが、ADO では特定のクエリ言語を使用する必要はありません。  
  
 シェイプコマンドは、**レコードセット**オブジェクトによって、または[Command](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトの[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティを設定して[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)メソッドを呼び出すことによって発行できます。  
  
 SQL JOIN 句を使用して、2つのテーブルを関連付けることができます。ただし、階層 **レコードセット** は、情報をより効率的に表すことができます。 結合によって作成された **レコードセット** の各行は、テーブルの1つから冗長な情報を繰り返します。 階層**レコードセット**には、複数の子**レコードセット**オブジェクトごとに1つの親**レコードセット**があります。  
  
 Shape コマンドは入れ子にすることができます。 つまり、 *親コマンド* または *子コマンド* 自体が別の shape コマンドになることがあります。  
  
 図形プロバイダーは、ユーザーが **Aduseserver**のカーソル位置を指定した場合でも、常にクライアントカーソルを返します。  
  
 形をした**レコードセット**の**レコードセット**コンポーネントには、プログラムから、または適切なビジュアルコントロールを使用してアクセスできます。  
  
 Microsoft では、図形のコマンドを生成するビジュアルツールを提供しています (Visual Basic 6 のドキュメントでは [データ環境デザイナー](/previous-versions/visualstudio/aa445793(v=vs.60)) を参照してください)。また、階層カーソルを表示する別のツールを提供します (Visual Basic 6 のドキュメントの「Microsoft 階層フレキシブルコントロールの使用」を参照してください)。  
  
 階層 **レコードセット**の移動の詳細については、「 [階層レコードセット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)」を参照してください。  
  
 構文的に正しい図形コマンドの詳細については、「 [仮形の文法](../../../ado/guide/data/formal-shape-grammar.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [集計関数、CALC 関数、NEW キーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [基になるデータ プロバイダーにコマンドを発行する](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)