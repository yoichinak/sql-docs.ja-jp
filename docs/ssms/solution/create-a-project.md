---
description: プロジェクトを作成する
title: プロジェクトを作成する
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 7e3bc58b9f702478bdef96535bc7c784d9e410df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497360"
---
# <a name="create-a-project"></a>プロジェクトを作成する

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
既存のソリューション内に、1 つ以上のプロジェクトを作成できます。  
  
## <a name="create-a-new-project-and-add-it-to-a-solution"></a>新しいプロジェクトを作成してソリューションに追加する  
  
1.  ソリューション エクスプローラーで、ソリューションを選択します。  
  
2.  **[ファイル]** メニューの **[追加]** をポイントし、 **[新しいプロジェクト]** をクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスで、プロジェクトの種類をクリックします。  
  
    **テンプレート**  
    **[テンプレート]** ボックスで、テンプレートを選択します。 **[テンプレート]** ボックスの下に、選択したプロジェクト テンプレートの簡単な説明が表示されます。  
  
    **名前**  
    作成するスクリプト プロジェクトの名前を入力します。 **[場所]** フィールドに表示された場所に、プロジェクトと同じ名前のフォルダーも作成されます。 プロジェクトによっては、ソース ファイルなどのサポート ファイルが [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] によって作成され、新しいプロジェクト フォルダーに追加されます。  
  
    > [!NOTE]  
    > 一部の種類のプロジェクトでは、場所を指定すると名前が設定されるため、 **[名前]** テキスト ボックスは使用できません。 たとえば、Web アプリケーションや Web サービスは Web サーバーに置かれ、名前はそのサーバーに指定されている仮想ディレクトリから付けられます。  
  
    次の文字は名前に使用できません。  
  
    -   シャープ記号 (#)  
  
    -   パーセント (%)  
  
    -   アンパサンド (&)  
  
    -   アスタリスク (*)  
  
    -   縦棒 (|)  
  
    -   円記号 (\\)  
  
    -   コロン (:)  
  
    -   引用符 (")  
  
    -   より小さい (\<)  
  
    -   より大きい (>)  
  
    -   疑問符 (?)  
  
    -   スラッシュ (/)  
  
    -   先頭または末尾の空白 (' ')  
  
    -   Microsoft Windows や MS-DOS で予約されている名前 ("nul"、"aux"、"con"、"com1"、"lpt1" など)  
  
    **場所**  
    プロジェクトを作成する場所を入力するか、一覧から場所を選択します。  
  
    **[参照]**  
    **[プロジェクトの場所]** ダイアログ ボックスを表示します。ここで、プロジェクトを保存する新しいディレクトリを指定できます。  
  
    **解決方法**  
    ソリューション エクスプローラーでソリューションを作成するには、 **[新しいソリューションを作成する]** を選択します。 ソリューション エクスプローラーで現在開いているソリューションに新しいプロジェクトを追加するには、 **[ソリューションに追加]** を選択します。  
  
    **[ソリューションのディレクトリを作成]**  
    オンにすると、 **[ソリューション名]** テキスト ボックスが有効になります。 プロジェクトとソリューションに指定した名前で新しいディレクトリが作成されます。  
  
    **[ソリューション名]**  
    プロジェクトを作成する、新しいソリューションの名前を入力します。 既定では、 **[名前]** フィールドに入力されている名前が使用されます。  
  
    **注** このオプションを使用するには、 **[ソリューション]** の **[新しいソリューションを作成する]** を選択し、 **[ソリューションのディレクトリを作成]** チェック ボックスをオンにする必要があります。 Web アプリケーションなど、一部のプロジェクト テンプレートでは、このオプションはサポートされません。  
  
    **[ソース管理に追加]**  
    このチェック ボックスをオンにすると、 **[OK]** をクリックしたときにソース管理アプリケーションが開きます。 ソース管理アプリケーションにより求められる情報をすべて入力します。 このオプションを使用するには、ソース管理クライアント アプリケーションをインストールしておく必要があります。  
  
4.  **[OK]** をクリックします。  
  
スクリプト プロジェクトの名前は設定できますが、フォルダー名は [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] によって設定され、変更できません。 **[新しいプロジェクトの追加]** ダイアログ ボックスを使用すると、共通のフォルダーのセットを示すドライブとパスを指定できます。 **ソリューション エクスプローラー**でソリューション アイコンを右クリックし、 **[追加]** をクリックします。 スクリプト プロジェクト フォルダーの既定の場所は、C:\Documents and Settings\\*username*\My Documents\SQL Server Management Studio\Projects\\です。  
  
## <a name="see-also"></a>参照

[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[ソリューションへの既存のプロジェクトの追加](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[プロジェクトへの新規項目の追加](../../ssms/solution/add-new-items-to-a-project.md)  
[既存の項目をプロジェクトに追加する](../../ssms/solution/add-existing-items-to-a-project.md)  
[プロジェクトの既定の場所の変更](../../ssms/solution/change-the-default-location-for-projects.md)  
[アイテムやプロジェクトのクリアまたは削除](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[ソリューションを削除する](../../ssms/solution/delete-a-solution.md)  
