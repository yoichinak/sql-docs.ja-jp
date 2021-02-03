---
title: FILESTREAM の有効化と構成 | Microsoft Docs
description: FILESTREAM を使用するには、まず、それを SQL Server データベース エンジン インスタンスで有効にします。 SQL Server 構成マネージャーを使用して FILESTREAM を有効にする方法を学習します。
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], enabling
ms.assetid: 78737e19-c65b-48d9-8fa9-aa6f1e1bce73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea678a62f4453232fe8442cf2053c3b951e361ef
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250661"
---
# <a name="enable-and-configure-filestream"></a>FILESTREAM の有効化と構成

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  FILESTREAM の使用を開始するには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスで FILESTREAM を有効にする必要があります。 このトピックでは、SQL Server 構成マネージャーを使用して FILESTREAM を有効にする方法について説明します。  
  
##  <a name="enabling-filestream"></a><a name="enabling"></a> FILESTREAM の有効化  
  
#### <a name="to-enable-and-change-filestream-settings"></a>FILESTREAM の設定の有効化と変更  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  サービスの一覧で、 **[SQL Server のサービス]** を右クリックし、 **[開く]** をクリックします。  
  
3.  **[SQL Server 構成マネージャー]** スナップインで、FILESTREAM を有効にする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを探します。  
  
4.  インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[SQL Server のプロパティ]** ダイアログ ボックスで、 **[FILESTREAM]** タブをクリックします。  
  
6.  **[Transact-SQL アクセスに対して FILESTREAM を有効にする]** チェック ボックスをオンにします。  
  
7.  Windows から FILESTREAM データの読み取りと書き込みを行う場合は、 **[ファイル I/O ストリーム アクセスに対して FILESTREAM を有効にする]** をクリックします。 Windows 共有の名前を **[Windows 共有名]** ボックスに入力します。  
  
8.  この共有に格納された FILESTREAM データにリモート クライアントからアクセスする必要がある場合は、 **[リモート クライアントに FILESTREAM データへのストリーム アクセスを許可する]** を選択します。  
  
9. **[Apply]** をクリックします。  
  
10. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[新しいクエリ]** をクリックしてクエリ エディターを表示します。  
  
11. クエリ エディターで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを入力します。  
  
    ```sql  
    EXEC sp_configure filestream_access_level, 2  
    RECONFIGURE  
    ```  
  
12. **[実行]** をクリックします。  
  
13. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再開します。  

##  <a name="best-practices"></a><a name="best"></a> ベスト プラクティス  
  
###  <a name="physical-configuration-and-maintenance"></a><a name="config"></a> 物理的な構成と保守  
 FILESTREAM ストレージ ボリュームを設定する場合は、次のガイドラインを考慮してください。  
  
-   FILESTREAM コンピューター システム上で短いファイル名を無効にします。 短いファイル名の作成には、長い時間がかかります。 短いファイル名を無効にするには、Windows **fsutil** ユーティリティを使用します。  
  
-   FILESTREAM コンピューター システムを定期的に最適化します。  
  
-   64 KB の NTFS クラスターを使用します。 圧縮されたボリュームは、4 KB の NTFS クラスターに設定する必要があります。  
  
-   FILESTREAM ボリューム上のインデックスの作成を無効にし、**disablelastaccess** を設定します。 **disablelastaccess** を設定するには、Windows **fsutil** ユーティリティを使用します。  
  
-   必要でない場合は、FILESTREAM ボリューム上でのウイルス スキャンを無効にします。 ウイルス スキャンが必要な場合は、問題のあるファイルを自動的に削除するポリシーを設定しないようにします。  
  
-   RAID レベルを設定および調整して、フォールト トレランスとアプリケーションで求められるパフォーマンスを実現します。  
  
|RAID レベル|書き込みパフォーマンス|読み取りパフォーマンス|フォールト トレランス|解説|  
|-|-|-|-|-|   
|RAID 5|Normal|Normal|[非常に良い]|パフォーマンスは、1 台のディスクまたは JBOD よりも高く、RAID 0 またはストライピング機能を備えた RAID 5 よりも低くなります。|  
|RAID 0|[非常に良い]|[非常に良い]|なし||  
|RAID 5 + ストライピング|[非常に良い]|[非常に良い]|[非常に良い]|最も高価なオプションです。|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
  
###  <a name="physical-database-design"></a><a name="database"></a> 物理的なデータベース設計  
 FILESTREAM データベースを設計するときは、次のガイドラインを考慮してください。  
  
-   FILESTREAM 列には対応する **uniqueidentifier** ROWGUID 列が存在する必要があります。 また、この種のテーブルには、一意なインデックスが存在する必要があります。 通常、このインデックスは、クラスター化インデックスではありません。 データベースのビジネス ロジックでクラスター化インデックスが求められる場合は、インデックスに格納されている値がランダムでないことを確認する必要があります。 格納されている値がランダムである場合、テーブルの行が追加または削除されるたびにインデックスの並べ替えが発生します。  
  
-   パフォーマンス上の理由から、FILESTREAM ファイル グループおよびコンテナーは、オペレーティング システム、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ、tempdb、ページング ファイル以外のボリュームに配置する必要があります。  
  
-   領域管理とポリシーは、FILESTREAM では直接サポートされません。 ただし、それぞれの FILESTREAM ファイル グループを別個のボリュームに割り当て、ボリュームの管理機能を使用することで、領域の管理とポリシーの適用を行うことができます。  
  
  
