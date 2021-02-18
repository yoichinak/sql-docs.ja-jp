---
title: トレース ファイルの最大ファイル サイズを設定する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler でトレース ファイルのサイズを制限する方法、およびファイルが最大サイズに達したときにロールオーバーするかどうかを指定する方法について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 094df80b40338af09e7c4d9084ec3715a91a61c5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345800"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>トレース ファイルの最大ファイル サイズの設定 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  トレース ファイルの最大ファイル サイズを設定するには、次の手順を実行します。  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>トレース ファイルの最大ファイル サイズを設定するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[テンプレート名]** ボックスの一覧で、トレース テンプレートを選択します。  
  
4.  **[ファイルに保存]** チェック ボックスをオンにし、トレース情報を格納するファイルを指定します。  
  
5.  **[最大ファイル サイズの設定 (MB)]** ボックスで、トレースの最大ファイル サイズを指定します。 ファイル サイズが指定した最大値に達すると、このファイルにはトレース イベントが記録されなくなります。 **[ファイル ロールオーバーを有効にする]** チェック ボックスをオンにした場合 (既定でオンになっています)、次の動作が行われます。  
  
     ファイルのロールオーバー オプションを使用すると、最大ファイル サイズに達したときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって現在のファイルが閉じられ、新しいファイルが作成されます。 新しいファイルの名前は古いファイルと同一ですが、順序を表す整数がファイル名に付加されます。たとえば、元のトレース ファイルの名前を filename_1.trc とすると、次のトレース ファイルは filename_2.trc となり、以降同様に続きます。 新しいロールオーバー ファイルに割り当てられた名前が既存のファイルで既に使用されている場合、その既存のファイルは、読み取り専用でない限り上書きされます。 トレース データをファイルに保存する場合、ファイルのロールオーバー オプションが既定で有効になります。  
  
     ファイルのロールオーバー オプションを有効にすると、トレースは他の方法によって停止されるまで続行されます。 ファイル サイズの制限に達した後でトレースを停止するには、ファイルのロールオーバー オプションを無効にします。  
  
    > [!NOTE]  
    >  FAT32 ファイル システムでは、ファイル サイズが 4 GB 弱に制限されます。 トレース ファイルがそのサイズに達すると、"ディスク領域が不足しています" というエラーが発生してトレースが失敗します。 これよりも大きなファイルを作成するには、NTFS ファイル システムを使用します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
