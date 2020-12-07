---
description: Azure SQL Database への接続 (アクセス先の SQL)
title: Azure SQL Database への接続 (アクセス先の SQL) |Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 15882852544113881b52f3641e0c85ec684add22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418568"
---
# <a name="connect-to-azure-sql-database-accesstosql"></a>Azure SQL Database への接続 (アクセス先の SQL)
[SQL Azure への接続] ダイアログボックスを使用して、移行する Azure SQL Database 内のデータベースに接続します。  
  
このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **SQL Azure に接続**] を選択します。 以前に接続している場合、コマンドは **SQL Azure に再接続します。**  
  
## <a name="options"></a>オプション  
**[サーバー名]**  
  
SQL Azure に接続するためのサーバー名を選択または入力します。  
  
**[データベース]**  
  
データベース名を選択、入力、または **参照** します。  
  
> [!IMPORTANT]  
> SSMA for Access は、SQL Azure の master データベースへの接続をサポートしていません。  
  
**ユーザー名**  
  
SSMA が接続に使用するユーザー名を入力し Azure SQL Database  
  
**パスワード**  
  
ユーザー名に対応するパスワードを入力します。  
  
**Encrypt**  
  
SSMA では、SQL Azure への暗号化接続を推奨しています。  
  
## <a name="create-database"></a>データベースの作成  
新しいデータベースを作成するには、次の手順に従います。  
  
1.  [SQL Azure への接続] ダイアログボックスに表示されている [参照] ボタンをクリックします。  
  
2.  データベースが存在しない場合は、2つのメニュー項目が表示されます。  
  
    1.  **(データベースが見つかりません)** が無効化され、常にグレー表示になっている  
  
    2.  常に有効になっている**新しいデータベースを作成**し、ユーザーが新しいデータベースを作成できるようにします。 このメニュー項目をクリックすると、[データベースの作成] ダイアログボックスにデータベースの名前とサイズが表示されます。  
  
3.  データベースの作成時に、これらの2つのパラメーターは入力として指定されます。  
  
    1.  **データベース名:** データベース名を入力します。  
  
    2.  **データベースサイズ:** SQL Azure アカウントで作成する必要のあるデータベースのサイズを選択します。  
  
