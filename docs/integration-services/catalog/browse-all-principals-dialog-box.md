---
description: '[すべてのプリンシパルを参照] ダイアログ ボックス'
title: '[すべてのプリンシパルを参照] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5ec280020b966a1d23b5ebb9dfb2c740692a6d1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123787"
---
# <a name="browse-all-principals-dialog-box"></a>[すべてのプリンシパルを参照] ダイアログ ボックス

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[すべてのプリンシパルを参照]** ダイアログ ボックスを使用して、データベースのプリンシパルを選択し、選択したプロジェクトに対する、または選択したフォルダーに格納されたすべてのプロジェクトに対するプリンシパルの権限を変更できます。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[すべてのプリンシパルを参照] ダイアログ ボックスを開く](#open_dialog)  
  
-   [オプションの構成](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> [すべてのプリンシパルを参照] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB カタログをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  選択したフォルダーに格納されたすべてのプロジェクトに対するプリンシパルの権限を変更するには、フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
     選択したプロジェクトに対するプリンシパルの権限を変更するには、プロジェクトが格納されているフォルダーを展開し、プロジェクトを右クリックして、 **[プロパティ]** をクリックします。  
  
5.  **[権限]** ページを選択し、 **[参照]** をクリックします。  
  
##  <a name="configure-the-options"></a><a name="options"></a> オプションの構成  
 このページには、SSISDB データベースのカタログ ビュー sys.database_principals から返されたプリンシパルが表示されます。  
  
 プリンシパルを選択した状態で、 **[OK]** をクリックして、 **[すべてのプリンシパルを参照]** ダイアログ ボックスを閉じると、そのプリンシパルが親ダイアログ ボックスの **[権限]** ページにある **[ログインまたはロール]** の一覧に追加されます。 **[ログインまたはロール]** の一覧にプリンシパルを追加すると、そのプリンシパルの選択したプロジェクトに対する権限を変更できます。  
  
 **[選択列]**  
 親ダイアログ ボックスの **[権限]** ページにある **[ログインまたはロール]** の一覧にプリンシパルを追加する場合はオンにします。  
  
 **[アイコン列]**  
 プリンシパルの **[種類]** に対応したアイコンです。  
  
 **名前**  
 プリンシパルの名前です。  
  
 **Type**  
 プリンシパルの種類。 一般的な種類を次に示します。  
  
-   SQL ユーザー  
  
-   Windows ユーザー  
  
-   データベース ロール  
  
  
