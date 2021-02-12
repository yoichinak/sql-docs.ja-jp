---
description: プロジェクトの設定 (Azure SQL Database) (MySQLToSQL)
title: プロジェクトの設定 (Azure SQL Database) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a5c3075180e60737931adfb1f544ace8bb38b9b0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100071866"
---
# <a name="project-settings-azure-sql-database-mysqltosql"></a>プロジェクトの設定 (Azure SQL Database) (MySQLToSQL)
SQL Azure のプロジェクト設定を使用すると、接続ダイアログに追加する Azure SQL Database サフィックスを構成し、SQL Azure 接続でハートビートメカニズムを実装することもできます。  
  
SQL Azure ウィンドウは、[プロジェクトの **設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   [プロジェクトの設定] ダイアログボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 SQL Azure 設定にアクセスするには、[ **ツール** ] メニューの [ **プロジェクトの設定**] を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **SQL Azure**] を選択します。  
  
-   [既定のプロジェクトの設定] ダイアログボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 SQL Azure 設定にアクセスするには、[ **ツール** ] メニューの [ **Defaultproject の設定**] を選択し、[移行先の **バージョン** ] ドロップダウンから [SQL Azure として移行プロジェクトの種類] を選択して SQL Azure ウィンドウの設定にアクセスし、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **SQL Azure**] を選択します。  
  
## <a name="options"></a>オプション  
  
## <a name="connectivity"></a>接続  
**ハートビートの間隔**  
  
SQL Azure 接続を ' 分: seconds ' 形式で保持するハートビートメカニズムに使用する時間間隔を指定します。  
  
**既定値**: ' 4:45 '  
  
値は、' m:ss ' 形式 (たとえば、' 4:45 ' または ' 0:50 ') で指定する必要があります。  
  
**SQL Azure サーバーサフィックス**  
  
SQL Azure サーバーのサフィックスを指定します  
  
**既定値**: ' database.windows.net '。  
  
