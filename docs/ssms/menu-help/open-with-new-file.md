---
description: '[ファイルを開くアプリケーションの選択] ([新しいファイル])'
title: '[ファイルを開くアプリケーションの選択] ([新しいファイル])'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Open With dialog box
ms.assetid: 9531588c-e7ec-4049-9f9c-ee000c49c5de
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cb7bd83a9a7526466d1a7798ab9ef3d71647d4fd
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037673"
---
# <a name="open-with-new-file"></a>[ファイルを開くアプリケーションの選択] ([新しいファイル])
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
1 つ以上のエディターでドキュメントを開くには、**[ファイル]** メニューの **[開く]** をクリックし、次に **[ファイル]** をクリックします。 **[ファイルを開く]** ダイアログ ボックスでファイルを選択し、 **[開く]** の横の矢印をクリックし、次に **[ファイルを開くアプリケーションの選択]** をクリックします。 **[ファイルを開くアプリケーションの選択]** ダイアログ ボックスの **[このファイルを開くのに使用するプログラムを選択してください]** の一覧で、目的のプログラムをクリックし、次に **[開く]** をクリックします。  
  
## <a name="options"></a>オプション  
**[このファイルを開くのに使用するプログラムを選択してください]**  
選択されているファイルの種類に対して [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio で利用可能なエディターを一覧表示します。 ドキュメントを開くために使用するエディターを一覧から選択するか、 **[追加]** をクリックして新しいエディターを一覧に含めます。  
  
**[ファイル]**  
**[開く]** をクリックすると、選択されたエディターでドキュメントが開きます。  
  
**追加**  
このボタンをクリックすると、 **[このファイルを開くのに使用するプログラムを選択してください]** の一覧にプログラムが追加されます。 **[プログラム名]** フィールドにプログラムへのファイル パスを入力するか、 **[参照]** をクリックしてプログラムの場所を指定します。 **[表示名]** に、 **[このファイルを開くのに使用するプログラムを選択してください]** の一覧に表示するプログラム名を入力します。  
  
**Remove**  
プログラムを削除するには、プログラムを選択して **[削除]** をクリックします。  
  
**[既定に設定]**  
選択したファイルの種類に対して既定のエディター (適用可能であれば言語エンコード オプションも) を指定するには、 **[このファイルを開くのに使用するプログラムを選択してください]** の一覧からプログラムを選択して **[既定に設定]** をクリックします。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でこのファイルの種類を次に開いたときには、新しい既定のエディターでドキュメントが開きます。  
  
> [!NOTE]  
> **[このファイルを開くのに使用するプログラムを選択してください]** のプログラムの一覧で、選択したファイルの種類の既定のエディターの名前には、 **(既定)** が末尾に付加されます。  
  
## <a name="see-also"></a>参照  
[ファイル拡張子をコード エディターに関連付ける](../scripting/associate-file-extensions-to-a-code-editor.md)