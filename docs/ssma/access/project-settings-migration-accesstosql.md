---
description: プロジェクトの設定 (移行) (Sql server への移行)
title: プロジェクトの設定 (移行) (Sql server への移行) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3163da352fa925a821287fc1447fd8b6b5e89cdb
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988498"
---
# <a name="project-settings-migration-accesstosql"></a>プロジェクトの設定 (移行) (Sql server への移行)
移行プロジェクトの設定を使用して、データを移行する方法や SQL Azure する方法を構成でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[移行] ウィンドウは、[ **プロジェクトの設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   [ **プロジェクトの設定** ] ダイアログボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 移行の設定にアクセスするには、[ **ツール** ] メニューの [ **プロジェクトの設定**] を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **移行**] をクリックします。  
  
-   [ **既定のプロジェクトの設定** ] ダイアログボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 移行設定にアクセスするには、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックし、設定にアクセスする [ **移行ターゲットバージョン** ] コンボボックスでプロジェクトの種類を選択して、左側のウィンドウの下部にある [ **全般** ] をクリックし、[ **移行**] をクリックします。  
  
## <a name="options"></a>オプション  
**CHECK 制約**  
データをテーブルに追加するときに SSMA が制約をチェックするかどうかを指定します。  
  
-   **既定のモード**: False  
  
-   **オプティミスティックモード**: True  
  
-   **フルモード**: False  
  
**[トリガーを起動する]**  
データをテーブルに追加するときに SSMA が挿入トリガーを起動するかどうかを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   **既定のモード**: False  
  
-   **オプティミスティックモード**: True  
  
-   **フルモード**: False  
  
**[ID を保持する]**  
にデータを追加するときに、SSMA がアクセス id の値を保持するかどうかを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 この値が False の場合、によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] id 値が割り当てられます。  
  
-   **既定のモード**: True  
  
-   **オプティミスティックモード**: True  
  
-   **フルモード**: False  
  
**[NULL を保持する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で指定されている既定値に関係なく、ソースデータのにデータを追加するときに、SSMA がソースデータ内の null 値を保持するかどうかを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   **既定のモード**: True  
  
-   **オプティミスティックモード**: False  
  
-   **フルモード**: True  
  
**テーブルロック**  
データ移行中にテーブルにデータを追加するときに SSMA がテーブルをロックするかどうかを指定します。 値が False の場合、SSMA では行ロックが使用されます。  
  
-   **既定のモード**: True  
  
-   **オプティミスティックモード**: True  
  
-   **フルモード**: True  
  
**サポートされていない日付の置換**  
SSMA が、最も古い datetime 日付よりも前のアクセス日付を修正する必要があるかどうかを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます (1753 年1月01日)。  
  
-   現在の日付の値を保持するには、[ **何もしない**] を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 列では、1753年1月01日より前の日付は受け付けられません。 古い日付を使用する場合は、datetime 値を文字値に変換する必要があります。  
  
-   1753年1月1日より前の日付を NULL に変換するには、[ **null で置換**] を選択します。  
  
-   1753年1月01日より前の日付をサポートされる日付に置き換えるには、[ **サポートされている最も近い日付で置き換える**] を選択します。 この値を選択した場合、既定では、サポートされている日付の最も近い日付が 01 January 1753 として選択されます。  
  
**バッチ サイズ**  
データ移行中に使用されるバッチサイズ。 トランザクションは、各バッチの後に記録されます。 既定では、すべてのスキームのバッチサイズは1万です。  
  
## <a name="see-also"></a>参照  
[ユーザーインターフェイスリファレンス (アクセス)](./user-interface-reference-accesstosql.md)  
