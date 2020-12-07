---
description: リンク ドメインの作成
title: リンク ドメインの作成
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.linkeddomain.f1
ms.assetid: fd99d422-c53d-4d7c-9cdd-303c703683b6
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 6dbe71b94bfc71cca727f34bb6a4fd4e532455bd
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725395"
---
# <a name="create-a-linked-domain"></a>リンク ドメインの作成

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でナレッジ ベースのリンク ドメインを作成する方法について説明します。 リンク ドメインとは、既存の別のドメインから作成されるドメインで、リンク先のドメインから値、ルール、およびプロパティ (名前と説明を除く) をすべて継承します。 リンク ドメインは 1 つのセットとしてまとめて管理できます。 ドメインを別のドメインにリンクすることで、他のドメインの内容を継承するドメインを作成することができます。  
  
## <a name="scenarios"></a>シナリオ  
 リンク ドメインは、次のようなシナリオで特に役立ちます。  
  
### <a name="mapping-multiple-fields-to-domains-that-share-values-rules-and-properties"></a>値、ルール、およびプロパティを共有するドメインに複数のフィールドをマップする  
 2 つのフィールドを同じドメインにマップすることはできません。ただし、一方のフィールドを 1 つのドメインにマップし、そのドメインにリンクされた別のドメインにもう一方のフィールドをマップすることができます。 これにより、内容とプロパティ (名前と説明を除く) が同じ 2 つの異なるドメインにそれらのフィールドがマップされます。 詳細については、「 [Map two fields to linked domains](#Map)」をご参照ください。  
  
### <a name="controlling-data-flow-to-composite-domains"></a>複合ドメインのデータ フローを制御する  
 リンク ドメインを使用すると、フィールドと複合ドメインの間のデータ フローを制御し、 複合ドメインに含まれるフィールドのデータ フローと、複合ドメインに含まれない非常によく似たフィールドのデータ フローを区別することができます。 これを実現するには、2 つのリンク ドメインの一方を複合ドメインに含め、もう一方を含めないように指定します。 ドメインの観点からは、リンク ドメインは同一であり、 どちらにも同じナレッジが含まれています。 ただし、複合ドメインの観点からは、リンク ドメインは同一ではなく、 一方は複合ドメインに含まれ、もう一方は含まれないという違いがあります。  
  
 たとえば、Customer First Name、Customer Last Name、および Father's First Name というフィールドを含むレコードがあるとします。 顧客の名と父親の名の両方を First Name ドメインにマップし、First Name ドメインと Last Name ドメインを Full Name 複合ドメインに含めるとすると、 姓がない複合ドメインに父親の名を追加することが問題になります。 この場合は、2 つの名のフィールドのそれぞれをドメインにリンクし、その 2 つのドメインをリンクすると、Customer First Name ドメインだけを Full Name 複合ドメインに追加し、Father's First Name フィールドは複合ドメインに追加しないようにすることができます。このようにすると、Father's First Name を複合ドメインに追加せずに済みます。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 リンク ドメインを作成するには、ナレッジ ベースとリンク先の既存のドメインが必要です。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 リンク ドメインを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="create-a-linked-domain"></a><a name="Create"></a> リンクドメインの作成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ナレッジ ベースを開くか作成します。 アクティビティとして **[ドメイン管理]** を選択した後に、 **[開く]** または **[作成]** をクリックします。 詳細については、「 [ナレッジ ベースの作成](../data-quality-services/create-a-knowledge-base.md) 」または「 [ナレッジ ベースを開く](../data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
3.  **[ドメイン管理]** ページの **[ドメイン リスト]** から、新しいドメインをリンクするドメインを右クリックし、 **[リンク ドメインの作成]** をクリックします。  
  
    > [!NOTE]  
    >  リンク ドメインを作成するための専用のアイコンはありません。 この操作は、コンテキスト メニューのコマンドでのみ実行できます。  
  
4.  **[ドメインの作成]** ダイアログ ボックスで、ナレッジ ベースに一意の名前と 256 文字までの説明を入力します。 リンク先のドメインの名前が正しいことを確認します。  
  
5.  **[OK]** をクリックしてリンク ドメインの作成を完了します。  
  
6.  必要に応じて、リンク ドメインの名前や説明を [ドメインのプロパティ] タブで変更できます。  
  
7.  **[完了]** をクリックし、「 [ドメイン管理アクティビティの終了](/previous-versions/sql/sql-server-2016/hh510411(v=sql.130))」の説明に従ってドメイン管理アクティビティを完了します。  
  
##  <a name="map-two-fields-to-linked-domains"></a><a name="Map"></a> Map two fields to linked domains  
  
1.  ナレッジ検出アクティビティでナレッジ ベースを開き、データベースとテーブルまたはビューにナレッジ ベースをマップします。  
  
2.  ドメインに 1 つのフィールドをマップした後、同じドメインにもう 1 つのフィールドをマップするように試行します。  
  
3.  ドメインが既に使用中であることを示すポップアップで、[はい] をクリックしてリンク ドメインを作成します。  
  
4.  [ドメインの作成] ダイアログ ボックスで、ドメインの名前と説明を入力し、[OK] をクリックします。  
  
##  <a name="follow-up-after-creating-a-linked-domain"></a><a name="FollowUp"></a> 補足情報: リンク ドメインの作成後  
 リンク ドメインを作成した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
##  <a name="behavior-of-a-linked-domain"></a><a name="Behavior"></a> リンク ドメインの動作  
 リンク ドメインの設定については、以下の変更が可能です。  
  
-   リンク ドメインの名前と説明を変更することができます。  
  
-   ドメインの **[データ型]**、 **[先頭の値を使用]**、または **[形式の出力先]** のプロパティを変更するには、リンク先のドメインを選択し、そのドメインの **[ドメインのプロパティ]** タブで設定を変更します。 これらの設定は、リンク ドメインのプロパティでは変更できません。 詳細については、「 [ドメインの作成](../data-quality-services/create-a-domain.md)」を参照してください。  
  
-   [ドメイン管理] ページの **[参照データ]** タブ、 **[ドメイン ルール]** タブ、 **[ドメイン値]** タブ、および **[用語ベースのリレーション]** タブの設定は、リンク ドメインとリンク先のドメインのどちらでも変更できます。一方を変更すると、もう一方に反映されます。  
  
 リンク ドメインには次の特性があります。  
  
-   2 つのドメインのリンクを解除することはできません。 リンクを解除するには、一方のリンク ドメインを削除します。  
  
-   [ドメイン管理] ページのドメイン リストでリンク ドメインを選択すると、 **"値"** テーブルを含むペインにリンク ドメインを識別する文字列が表示され、リンク ドメインであることが示されます。  
  
-   別のドメインがリンクされているドメインを削除した場合、両方のドメインが削除されます。 ただし、リンク ドメインを削除した場合は、リンク先のドメインは削除されません。  
  
-   別のドメインにリンクされたドメインにリンク ドメインをリンクすることはできません。  
  
-   複合ドメインに対するリンク ドメインまたはリンク複合ドメインは作成できません。  
  
-   [ドメイン管理] のいずれかのタブでリンク ドメインをダブルクリックすると、ドメインが編集用に開き、リンク ドメインであることを示す名前の文字列が表示されます。  
  
