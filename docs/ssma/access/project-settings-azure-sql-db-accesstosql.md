---
description: プロジェクトの設定 (Azure SQL Database) (SQL server による)
title: プロジェクトの設定 (Azure SQL Database) (SQL server による) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9954fe012158526e87bd30512b13eca0314bc00e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418548"
---
# <a name="project-settings-azure-sql-database-accesstosql"></a>プロジェクトの設定 (Azure SQL Database) (SQL server による)
SQL Azure のプロジェクト設定を使用すると、接続ダイアログに追加する Azure SQL Database サフィックスを構成し、SQL Azure 接続でハートビートメカニズムを実装することもできます。  
  
SQL Azure ウィンドウは、[プロジェクトの **設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   [プロジェクトの設定] ダイアログボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 SQL Azure 設定にアクセスするには、[ **ツール** ] メニューの [ **プロジェクトの設定**] を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **SQL Azure**] を選択します。  
  
-   [既定のプロジェクトの設定] ダイアログボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 SQL Azure 設定にアクセスするには、[ **ツール** ] メニューの [ **Defaultproject の設定**] を選択し、[ **移行先のバージョン** ] コンボボックスで [SQL Azure] としてプロジェクトの種類を選択して SQL Azure ウィンドウの設定にアクセスします。次に、左側のウィンドウの下部にある [ **全般** ] をクリックし、[ **SQL Azure**] を選択します。  
  
## <a name="options"></a>オプション  
  
## <a name="connectivity"></a>接続  
**ハートビートの間隔**  
  
SQL Azure 接続を ' 分: seconds ' 形式で保持するハートビートメカニズムに使用する時間間隔を指定します。  
  
**既定値**: ' 4:45 '  
  
値は、' m:ss ' 形式 (たとえば、' 4:45 ' または ' 0:50 ') で指定する必要があります。  
  
**SQL Azure サーバーサフィックス**  
  
SQL Azure サーバーのサフィックスを指定します  
  
**既定値**: ' database.windows.net '。  
  
