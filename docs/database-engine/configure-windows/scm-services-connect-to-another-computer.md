---
title: 別のコンピューターへの接続 (SQL Server 構成マネージャー) | Microsoft Docs
description: リモート コンピューターのサービスを管理する方法について説明します。 SQL Server 構成マネージャーまたは SQL Server Management Studio 使用してこのタスクを行う方法を説明します。
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b178e38f6e59499ddf74e9a8aaec037bbaa4d442
ms.sourcegitcommit: 2f3f5920e0b7a84135c6553db6388faf8e0abe67
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98783443"
---
# <a name="scm-services---connect-to-another-computer"></a>SCM サービス - 別のコンピューターに接続する

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この記事では、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] で別のコンピューターに接続する方法について説明します。 Windows の [コンピューターの管理] の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) を開くための最初の手順に従って、コンピューターに接続し、[サービスとアプリケーション] ツリーを展開します。 2 番目の手順に従って、リモート コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーへのリンクを含むファイルを作成します。

> [!NOTE]
> リモートで接続している場合、一部の操作は構成マネージャーで実行することができません。

別のコンピューターのサービスを開始、停止、一時停止、または再開するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してサーバーに接続し、サーバーまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを右クリックし、次に目的の操作をクリックします。

## <a name="SSMSProcedure"></a>

### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>Windows のコンピューターの管理を使用して別のコンピューターに接続するには

1. **[スタート]** メニュー ボタンを右クリックし、 **[コンピューターの管理 (ローカル)]** をクリックします。
2. **[操作]** メニューの **[別のコンピューターへ接続]** をクリックします。
3. **[コンピューターの選択]** ダイアログ ボックスの **[別のコンピューター]** ボックスに管理するコンピューターの名前を入力し、 **[OK]** をクリックします。

   リモート コンピューターで実行されているサービスが、[コンピューターの管理] に表示されます。 最上位ノードが **[コンピューターの管理** ]\<*remotecomputer*> に変更されます。

4. コンソール ツリーの **[サービスとアプリケーション]** を展開し、 **[SQL Server 構成マネージャー]** を展開して、リモート コンピューターのサービスを管理します。

### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>別のコンピューターの SQL Server 構成マネージャーへのリンクを保存するには

1. **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。

2. **[名前]** ボックスに「**mmc -a**」と入力 (64 ビット コンピューター上では「**mmc /32 -a**」と入力) して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソールを作成者モードで開きます。
3. **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。
4. **[スナップインの追加と削除]** ウィンドウで **[追加]** をクリックします。
5. **[スタンドアロン スナップインの追加]** ウィンドウで **[コンピューターの管理]** をクリックし、次に **[追加]** をクリックします。
6. **[コンピューターの管理]** ウィンドウの **[別のコンピューター]** をクリックし、管理するリモート コンピューターの名前を入力して **[完了]** をクリックします。
7. **[スタンドアロン スナップインの追加]** ウィンドウで **[閉じる]** をクリックします。
8. **[スナップインの追加と削除]** ウィンドウで **[OK]** をクリックします。
9. **[コンピューターの管理 (** _\<computer name>_ **)]** と **[サービスとアプリケーション]** を展開します。
10. **[SQL Server 構成マネージャー]** を右クリックして、 **[ここから新しいウィンドウ]** をクリックします。
11. **[ウィンドウ]** メニューの **[コンソール ルート]** をクリックし、最初のウィンドウに切り替えてからそのウィンドウを削除します。
12. **[ファイル]** メニューの **[名前を付けて保存]** をクリックし、ファイルにファイル拡張子 **.msc** を含む適切なファイル名を付けて目的のフォルダーに保存します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソールを閉じます。
13. ターゲット コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、そのファイルをダブルクリックします。 必要な場合は、デスクトップまたは **[スタート]** メニューにファイルへのリンクを保存します。

> [!CAUTION]
> リモート コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用する場合、コンピューター名が明らかではないため、誤って別のコンピューターを停止または構成してしまう可能性があります。 サービスを変更する前に、 **[サービス]** タブの **[ホスト名]** ボックスを調べてコンピューター名を確認してください。

## <a name="see-also"></a>関連項目

- [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)
