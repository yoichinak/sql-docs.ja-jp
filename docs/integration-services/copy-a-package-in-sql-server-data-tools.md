---
description: SQL Server Data Tools でのパッケージのコピー
title: SQL Server Data Tools でのパッケージのコピー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2bdd78011dc51986691ac31b031735d766dd6f5a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194896"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools でのパッケージのコピー

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  このトピックでは、既存のパッケージをコピーして新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成する方法、および新しいパッケージの **Name** プロパティと **GUID** プロパティを更新する方法について説明します。  
  
### <a name="to-copy-a-package"></a>パッケージをコピーするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、コピーするパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックします。  
  
3.  コピーするパッケージがソリューション エクスプローラーで選択されていること、またはパッケージが含まれている SSIS デザイナーのタブがアクティブになっていることを確認します。  
  
4.  **[ファイル]** メニューの **[名前を付けて \<package name> を保存]** をクリックします。  
  
    > [!NOTE]  
    >  **[ファイル]** メニューに **[名前を付けて保存]** オプションを表示するには、SSIS デザイナーでパッケージを開いておく必要があります。  
  
5.  必要に応じて、別のフォルダーを参照します。  
  
6.  パッケージ ファイルの名前を更新します。 ファイル拡張子は、必ず .dtsx のままにしておきます。  
  
7.  **[保存]** をクリックします。  
  
8.  プロンプトで、パッケージ オブジェクトの名前をファイル名と一致するように更新するかどうかを選択します。 **[はい]** をクリックすると、パッケージの **Name** プロパティが更新されます。 新しいパッケージが [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに追加され、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで開かれます。  
  
9. 必要に応じて、 **[制御フロー]** タブの背景をクリックし、 **[プロパティ]** をクリックします。  
  
10. [プロパティ] ウィンドウで、ID プロパティの値をクリックし、ドロップダウン リストの **[\<Generate New ID>]** をクリックします。  
  
11. **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックし、新しいパッケージを保存します。  
  
## <a name="see-also"></a>参照  
 [パッケージのコピーを保存する](./save-packages.md)   
 [SQL Server データ ツールでのパッケージの作成](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; パッケージ](../integration-services/integration-services-ssis-packages.md)  
  
