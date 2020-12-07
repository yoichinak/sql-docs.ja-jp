---
description: ドメインの作成
title: ドメインの作成
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 399cc88598173e7406b326c83ea9a098b879c59e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725362"
---
# <a name="create-a-domain"></a>ドメインの作成

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でドメインを作成する方法について説明します。 ドメインの値は、フィールド内のデータのセマンティック表現です。 ドメインについて詳しくは、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」をご覧ください。  
  
 新しいドメインを作成するには、次の 2 つの方法があります。 1 つ目は、ナレッジ検出アクティビティのマップ手順中に、データ サンプルを分析する過程でナレッジを新しいまたは既存のナレッジ ベースに追加するときに行います。 2 つ目は、ドメイン管理アクティビティの実行中に、既存のドメインを変更するのではなく、新しいドメインを作成するときに行います。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ドメインを作成するには、ナレッジ ベースを作成して開いておく必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ドメインを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator が必要です。  
  
##  <a name="create-a-domain-in-the-knowledge-discovery-activity"></a><a name="Discovery"></a> ナレッジ検出アクティビティでのドメインの作成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[ナレッジ ベースを開く]** をクリックし、ナレッジ ベースを選択するか、 **[新しいナレッジ ベース]** をクリックし、新しいナレッジ ベースのプロパティを入力します。  
  
3.  アクティビティとして **[ナレッジ検出]** を選択した後に、 **[作成]** をクリックして新しいナレッジ ベースを作成するか、 **[開く]** をクリックして既存のナレッジ ベースを開きます。  
  
4.  **[マップ]** ページで、データ ソースへの接続を指定します。 詳細については、「 [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md)」をご参照ください。  
  
5.  **"マッピング"** テーブルで、空の行の **[ソース列]** 列のドロップダウン リストからソース列を選択します。 対応するドメインが存在しない場合は、 **[ドメインの作成]** アイコンをクリックします。  
  
##  <a name="create-a-domain-in-the-domain-management-activity"></a><a name="DomainManagement"></a> ドメイン管理アクティビティでドメインを作成する  
  
1.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[ナレッジ ベースを開く]** をクリックし、ナレッジ ベースを選択するか、 **[新しいナレッジ ベース]** をクリックし、新しいナレッジ ベースのプロパティを入力します。  
  
2.  アクティビティとして **[ドメイン管理]** を選択した後に、 **[作成]** をクリックして新しいナレッジ ベースを作成するか、 **[開く]** をクリックして既存のナレッジ ベースを開きます。  
  
3.  **[ドメイン管理]** ページで、ドメイン リストの上にある **[ドメインの作成]** アイコンをクリックします。  
  
##  <a name="set-domain-properties"></a><a name="Properties"></a> ドメインのプロパティの設定  
  
1.  **[ドメインの作成]** ダイアログ ボックスで、ナレッジ ベースに一意の名前と 256 文字までの説明を入力します。  
  
    > [!NOTE]  
    >  ドメインのプロパティの詳細については、「 [Set Domain Properties](../data-quality-services/set-domain-properties.md)」を参照してください。  
  
2.  **[データ型]** の一覧で、ドメイン内の値に対するデータ型を選択します。 データ型には、 **[String]** (既定値)、 **[Date]**、 **[Integer]**、または **[Decimal]** を指定できます。  
  
3.  シノニムの値ではなく、シノニムのグループの先頭の値が出力されることを指定する場合は、 **[先頭の値を使用]** をオンにします。 各シノニムの値が正しいフォームまたは修正されたフォームで出力され、そのグループの先頭の値で置き換えられないことを指定する場合は、 **[先頭の値を使用]** をオフにします。  
  
4.  データ型が **[String]** の場合は、 **[文字列を正規化する]** をオンにしてドメイン値の特殊文字を削除すると、一致の可能性が高まる場合があります。  
  
5.  **[形式の出力先]** ボックスの一覧で、ドメイン内のデータ値が出力されるときに適用される書式設定を選択します。 書式設定は、次の一覧に示すように手順 2. で選択されたデータ型に固有です。  
  
    -   文字列値の場合は、出力する文字列を大文字、小文字、または先頭文字のみ大文字として指定できます。  
  
    -   日付値の場合は、日、月、および年の形式を指定できます。  
  
    -   整数値の場合は、適用される形式マスクの種類を指定できます。  
  
    -   10 進数値の場合は、適用される精度と形式マスクの種類を指定できます。  
  
     **[形式の出力先]** ボックスで **[なし]** をクリックすると、一覧のどの書式設定も適用されません。  
  
6.  データ型が **[String]** の場合は、 **[言語]** ボックスの一覧で、スペル チェックを有効にした場合に適用するスペル チェックの言語バージョンを選択します。  
  
7.  データ型が **[String]** の場合は、 **[スペル チェックを有効にする]** をオンにして、ドメインを設定するときにすべての文字列値に対してスペル チェックを実行します。  
  
8.  データ型が **[String]** の場合は、 **[構文エラーのアルゴリズムを無効にする]** をオンにして、文字列値の構文エラーをチェックせずにドメインを設定します。  
  
9. **[OK]** をクリックします。  
  
10. **[完了]** をクリックし、「 [ドメイン管理アクティビティの終了](/previous-versions/sql/sql-server-2016/hh510411(v=sql.130))」の説明に従ってドメイン管理アクティビティを完了します。  
  
##  <a name="follow-up-after-creating-a-domain"></a><a name="FollowUp"></a> 補足情報: ドメインを作成した後  
 ドメインを作成した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
