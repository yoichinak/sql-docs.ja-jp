---
description: バックアップの管理 (SybaseToSQL)
title: バックアップの管理 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Managing Backups
ms.assetid: 266d987c-ecc5-4fa4-bfdf-8c584f1a1332
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1c29cec3ec38dc56636df0c3f063f4a758e6e87e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100017302"
---
# <a name="managing-backups-sybasetosql"></a>バックアップの管理 (SybaseToSQL)
Sybase のバックアップ管理を使用すると、テストの実行前または実行後にテーブルデータをバックアップおよび復元できます。 [バックアップコンテンツの管理] ダイアログボックスを使用して、バックアップコンテンツを管理することもできます。  
  
## <a name="sybase-backup-management"></a>Sybase のバックアップ管理  
  
### <a name="backup"></a>バックアップ  
[バックアップ] ダイアログを開くには、[テスト担当者] メニューの [Sybase Backup Management] をポイントし、[バックアップ...] をクリックします。[バックアップ] ダイアログボックスに、読み込まれた Sybase スキーマのすべてのテーブルを表示する Sybase メタデータツリーが表示されます。 バックアップを実行する1つ以上のテーブルを選択します。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   [ **バックアップ** ] ボタンをクリックして、テーブルのデータをバックアップします。  
  
-   [ **キャンセル** ] ボタンをクリックして、ダイアログを閉じます。  
  
### <a name="restore"></a>復元  
[復元] ダイアログを開くには、[テスト担当者] メニューの [Sybase Backup Management] をポイントし、[復元...] をクリックします。ここには、バックアップで使用可能なテーブルを含むツリーが表示されます。 データを復元する1つ以上のテーブルを選択します。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   バックアップデータをテーブルに復元するには、[ **復元** ] ボタンをクリックします。  
  
-   [ **キャンセル** ] ボタンをクリックして、ダイアログを閉じます。  
  
### <a name="managing-backup-contents"></a>バックアップコンテンツの管理  
バックアップコンテンツの管理を開くには、[テスト担当者] メニューの [Sybase Backup Management] をポイントし、[コンテンツのバックアップ] をクリックします。この場所には、バックアップ内のテーブルを含むツリーが表示されます。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   バックアップからテーブルを削除するには、[ **削除** ] ボタンをクリックします。  
  
-   [ **閉じる** ] ボタンをクリックして、ダイアログを閉じます。  
  
## <a name="sql-server-backup-management"></a>バックアップ管理の SQL Server  
SQL Server バックアップ管理を使用すると、テストの実行前または実行後にテーブルデータをバックアップおよび復元できます。 [バックアップコンテンツの管理] ダイアログボックスを使用して、バックアップコンテンツを管理することもできます。  
  
### <a name="backup"></a>バックアップ  
[バックアップ] ダイアログを開くには、[テスト担当者] メニューの [SQL Server バックアップの管理] をポイントし、[バックアップ] をクリックします。 [バックアップ] ダイアログボックスに、読み込まれた SQL Server データベースのすべてのテーブルを表示している SQL Server メタデータツリーが表示されます。 バックアップを実行する1つ以上のテーブルを選択します。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   [ **バックアップ** ] ボタンをクリックして、テーブルのデータをバックアップします。  
  
-   [ **キャンセル** ] ボタンをクリックして、ダイアログを閉じます。  
  
### <a name="restore"></a>復元  
[復元] ダイアログを開くには、[テスト担当者] メニューの [SQL Server バックアップの管理] をポイントし、[復元...] をクリックします。ここには、バックアップで使用可能なテーブルを含むツリーが表示されます。 データを復元するテーブルを1つ以上選択します。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   バックアップデータをテーブルに復元するには、[ **復元** ] ボタンをクリックします。  
  
-   [ **キャンセル** ] ボタンをクリックして、ダイアログを閉じます。  
  
### <a name="managing-backup-contents"></a>バックアップコンテンツの管理  
バックアップコンテンツの管理を開くには、[テスト担当者] メニューの [SQL Server バックアップの管理] をポイントし、[コンテンツのバックアップ] をクリックします。この場所には、バックアップ内のテーブルを含むツリーが表示されます。  
  
ダイアログでは、次のボタンを使用できます。  
  
-   [ **状態の確認** ] ボタンをクリックして、テーブルのバックアップ状態を確認します。  
  
-   バックアップからテーブルを削除するには、[ **削除** ] ボタンをクリックします。  
  
-   [ **閉じる** ] ボタンをクリックして、ダイアログを閉じます。  
  
## <a name="see-also"></a>参照  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
