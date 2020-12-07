---
description: Azure SQL Database への接続 (SybaseToSQL)
title: Azure SQL Database への接続 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3717cce895ca602a550d47ea5c569af4c80963a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492315"
---
# <a name="connect-to-azure-sql-database--sybasetosql"></a>Azure SQL Database への接続 (SybaseToSQL)
[Azure SQL Database への接続] ダイアログボックスを使用して、移行する Azure SQL Database データベースに接続します。  
  
このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **Azure SQL Database に接続**] を選択します。 以前に接続している場合、コマンドは **Azure SQL Database に再接続します。**  
  
## <a name="options"></a>オプション  
**[サーバー名]**  
  
Azure SQL Database に接続するためのサーバー名を選択または入力します。  
  
**[データベース]**  
  
データベース名を選択、入力、または **参照** します。  
  
> [!IMPORTANT]  
> SSMA for Sybase は、Azure SQL Database の master データベースへの接続をサポートしていません。  
  
**ユーザー名**  
  
SSMA が Azure SQL Database データベースへの接続に使用するユーザー名を入力します。  
  
**パスワード**  
  
ユーザー名に対応するパスワードを入力します。  
  
**Encrypt**  
  
SSMA では、Azure SQL Database への暗号化接続を推奨しています。  
  
## <a name="create-azure-database"></a>Azure データベースの作成  
Azure SQL Database アカウントにデータベースがない場合は、最初のデータベースを作成できます。  
  
初めて新しいデータベースを作成するには、次の手順に従います。  
  
1.  [Azure SQL Database への接続] ダイアログボックスに表示されている [参照] ボタンをクリックします。  
  
2.  データベースが存在しない場合は、次の2つのメニュー項目が表示されます。  
  
    1.  **(データベースが見つかりません)** が無効化され、常にグレー表示になっている  
  
    2.  Azure SQL Database アカウントにデータベースが存在しない場合にのみ有効になる**新しいデータベースを作成**します。 このメニュー項目をクリックすると、[Azure データベースの作成] ダイアログボックスにデータベースの名前とサイズが表示されます。  
  
3.  データベースの作成時には、次の2つのパラメーターが入力として指定されます。  
  
    1.  **データベース名:** データベース名を入力します。  
  
    2.  **データベースサイズ:** Azure SQL Database アカウントで作成する必要のあるデータベースのサイズを選択します。  
  
