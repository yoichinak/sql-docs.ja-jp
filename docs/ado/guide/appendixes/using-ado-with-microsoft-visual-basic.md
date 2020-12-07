---
description: Microsoft Visual Basic および Visual Basic for Applications での ADO の使用
title: Microsoft Visual Basic で ADO を使用する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e2076732536c8d9862ebc022f7a78b197ff428c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990973"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic および Visual Basic for Applications での ADO の使用
Visual Basic と Visual Basic for Applications のどちらを使用する場合でも、ADO プロジェクトの設定と ADO コードの記述は似ています。 このトピックでは、Visual Basic と Visual Basic for Applications の両方で ADO を使用する方法について説明し、相違点について説明します。

## <a name="referencing-the-ado-library"></a>ADO ライブラリの参照
 ADO ライブラリは、プロジェクトによって参照されている必要があります。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic から ADO を参照するには

1.  Visual Basic で、[ **プロジェクト** ] メニューの [ **参照**] を選択します。

2.  一覧から [ **Microsoft ActiveX データオブジェクト2.X ライブラリ** ] を選択します。 少なくとも次のライブラリが選択されていることを確認します。

    -   Visual Basic for Applications

    -   Visual Basic ランタイムオブジェクトとプロシージャ

    -   Visual Basic のオブジェクトとプロシージャ

    -   OLE オートメーション

3.  **[OK]** をクリックします。

 ADO は、たとえば、Microsoft Access を使用して、Visual Basic for Applications と同様に簡単に使用できます。

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access から ADO を参照するには

1.  Microsoft Access で、**データベース**ウィンドウの [**モジュール**] タブでモジュールを選択または作成します。

2.  [ **ツール** ] メニューの [ **参照**] をクリックします。

3.  一覧から [ **Microsoft ActiveX データオブジェクト2.X ライブラリ** ] を選択します。 少なくとも次のライブラリが選択されていることを確認します。

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 オブジェクトライブラリ (またはそれ以降)

    -   Microsoft DAO 3.5 オブジェクトライブラリ (またはそれ以降)

4.  **[OK]** をクリックします。

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic での ADO オブジェクトの作成
 この変数のオートメーション変数とオブジェクトのインスタンスを作成するには、 **Dim** または **CreateObject**の2つのメソッドを使用できます。

### <a name="dim"></a>Dim
 **Dim**で**New**キーワードを使用すると、1回の手順で ADO オブジェクトのインスタンスを宣言および作成できます。

```
Dim conn As New ADODB.Connection
```

 また、 **Dim** ステートメントの宣言とオブジェクトのインスタンス化も、次の2つの手順になります。

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  `ADODB`プロジェクトで ADO ライブラリを正しく参照している場合は、 **Dim**ステートメントで progid を明示的に使用する必要はありません。 ただし、これを使用すると、他のライブラリとの名前の競合を防ぐことができます。

> [!NOTE]
>  たとえば、同じプロジェクトに ADO と DAO の両方への参照を含める場合は、次のコードのように、 **レコードセット** オブジェクトをインスタンス化するときに使用するオブジェクトモデルを指定するための修飾子を含める必要があります。

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 **CreateObject**メソッドでは、宣言とオブジェクトのインスタンス化は、次の2つの独立した手順でなければなりません。

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 **CreateObject**でインスタンス化されたオブジェクトは遅延バインディングされます。つまり、厳密に型指定されていないため、コマンドライン補完は無効になります。 ただし、プロジェクトから ADO ライブラリを参照することはできません。また、特定のバージョンのオブジェクトをインスタンス化することができます。 次に例を示します。

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 これを行うには、特に ADO バージョン2.0 タイプライブラリへの参照を作成し、オブジェクトを作成します。

 **CreateObject**メソッドを使用したオブジェクトのインスタンス化は、通常、 **Dim**ステートメントを使用するよりも遅くなります。

## <a name="handling-events"></a>イベントの処理
 Microsoft Visual Basic で ADO イベントを処理するには、 **WithEvents** キーワードを使用してモジュールレベルの変数を宣言する必要があります。 変数は、クラスモジュールの一部としてのみ宣言でき、モジュールレベルで宣言する必要があります。 ADO イベントの処理の詳細については、「 [Ado イベントの処理](../data/handling-ado-events.md)」を参照してください。

## <a name="visual-basic-examples"></a>Visual Basic の例
 ADO ドキュメントには、多くの Visual Basic の例が含まれています。 詳細については、「 [Microsoft Visual Basic の ADO コード例](../../reference/ado-api/ado-code-examples-in-visual-basic.md)」を参照してください。

## <a name="see-also"></a>参照
 [Microsoft ActiveX データオブジェクト (ado)](../../microsoft-activex-data-objects-ado.md) [と](./using-ado-with-microsoft-visual-c.md)ado を使用して[スクリプト言語で ado を](./using-ado-with-scripting-languages.md)使用する Microsoft Visual C++