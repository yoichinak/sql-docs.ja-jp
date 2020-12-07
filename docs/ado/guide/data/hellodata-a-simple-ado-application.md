---
description: 'HelloData: 単純な ADO アプリケーション'
title: 'HelloData: 単純な ADO アプリケーション |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: rothja
ms.author: jroth
ms.openlocfilehash: bec2b55f7daee865489c3f32e1ee70e53b9102a6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980633"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: 単純な ADO アプリケーション
この単純なアプリケーションでは、データの取得、検査、編集、および更新の4つの主要な ADO 操作を実行します。 これらの操作は、Microsoft® SQL Server に含まれる Northwind サンプルデータベースに対して実行されます。 ADO の基礎に注目し、コードが乱雑にならないようにするために、この例のエラー処理は最小限に抑えられています。  
  
### <a name="to-run-hellodata"></a>HelloData を実行するには  
  
1.  ADO ライブラリを参照する新しい標準 EXE Visual Basic プロジェクトを作成します。 詳細については、「 [ADO ライブラリの参照](../referencing-the-ado-libraries.md)」を参照してください。  
  
2.  フォームの上部に4つのコマンドボタンを作成し、このトピックの最後にある表に示すように、 **Name** プロパティと **Caption** プロパティに値を設定します。  
  
3.  ボタンの下に、 **Microsoft DataGrid コントロール** (Msdatgrd) を追加します。 Msdatgrd ファイルは Visual Basic に含まれており、\windows\system32 または \winnt\system32 ディレクトリにあります。 DataGrid コントロールを Visual Basic ツールボックスウィンドウに追加するには、[**プロジェクト**] メニューの [**コンポーネント**] をクリックします。 次に、[Microsoft DataGrid コントロール 6.0 (SP3) (OLEDB)] の横にあるチェックボックスをオンにして、[ **OK]** をクリックします。 コントロールをプロジェクトに追加するには、DataGrid コントロールをツールボックスから Visual Basic フォームにドラッグします。  
  
4.  次の表に示すように、グリッドの下のフォームに **テキストボックス** を作成し、そのプロパティを設定します。 完了すると、フォームは次の図のようになります。  
  
5.  最後に、 [HelloData コード](./hellodata-code.md)に一覧表示されているコードをコピーし、フォームのコードエディターウィンドウに貼り付けます。 **F5**キーを押してコードを実行します。  
  
> [!NOTE]
>  次の例では、ガイド全体を通して、ユーザー id "MyId" とパスワード "123aBc" を使用してサーバーに対する認証を行います。 これらの値は、サーバーの有効なログオン資格情報に置き換える必要があります。 また、"MySQLServer" の値をサーバーの名前に置き換えます。  
  
 コードの詳細については、 [HelloData に関するコメント](./comments-on-hellodata.md)を参照してください。  
  
 ![HelloData VB アプリケーションの Form1](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|コントロール型|プロパティ|[値]|  
|------------------|--------------|-----------|  
|フォーム|Name|Form1|  
||[高さ]|6500|  
||幅|6500|  
|MS DataGrid|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||Multiline|true|  
|コマンドボタン|Name|cmdGetData|  
||Caption|Get Data|  
|コマンドボタン|Name|cmdExamineData|  
||Caption|データの調査|  
|コマンドボタン|Name|cmdEditData|  
||Caption| データの編集|  
|コマンドボタン|Name|cmdUpdateData|  
||Caption|更新データ|