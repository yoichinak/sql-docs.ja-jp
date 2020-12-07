---
description: ドメインのプロパティの設定
title: ドメインのプロパティの設定
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.domainproperties.f1
ms.assetid: 8a3c88ca-31d6-4f75-9aca-cf027c6d9845
author: swinarko
ms.author: sawinark
ms.openlocfilehash: a229aacb9110bdd5eefa9dc3987ce39fec8a1e66
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726623"
---
# <a name="set-domain-properties"></a>ドメインのプロパティの設定

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でドメインのプロパティを設定する方法について説明します。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ドメインのプロパティを設定するには、ナレッジ ベースとドメインを作成しておく必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ドメインのプロパティを設定するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールを所有している必要があります。  
  
##  <a name="set-domain-properties"></a><a name="Set"></a> ドメインのプロパティの設定  
  
1.  ドメイン管理アクティビティでナレッジ ベースを開き (「 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)」を参照)、 **[ドメイン]** ボックスの一覧で適切なドメインを選択して、既存のドメインにプロパティを設定します。 [ドメインのプロパティ] ページは、既定で表示されます。  
  
2.  「 [Create a Domain](../data-quality-services/create-a-domain.md)」の説明に従って新しいドメインを作成した後に、そのドメインにプロパティを設定します。  
  
3.  **[完了]** をクリックし、「 [ドメイン管理アクティビティの終了](/previous-versions/sql/sql-server-2016/hh510411(v=sql.130))」の説明に従ってドメイン管理アクティビティを完了します。  
  
##  <a name="follow-up-after-setting-domain-properties"></a><a name="FollowUp"></a> 補足情報: ドメインのプロパティを設定した後  
 ドメインのプロパティを設定した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
##  <a name="domain-properties"></a><a name="Properties"></a> ドメインのプロパティ  
  
###  <a name="domain-name-and-description"></a><a name="Name"></a> ドメイン名と説明  
 ドメインを作成した後に、ドメインの名前または説明を変更できます。 ドメイン名は、ナレッジ ベースに対して一意である必要があります。 説明は 256 文字まで指定できます。  
  
###  <a name="data-type"></a><a name="Type"></a> データ型  
 ドメインを作成する場合、ドメインの値のデータ型として **[String]** (既定値)、 **[Date]**、 **[Integer]**、 **[Decimal]** のいずれか 1 つを選択します。 ドメインを作成した後は、データ型を表示することはできますが、変更することはできません。 ドメイン用に選択したデータ型によって、ドメインにマップできるソース データの型が定義されます。 DQS の 4 つのドメイン データ型のそれぞれでサポートされているデータ型については、「[DQS ドメインに対してサポートされる SQL Server のデータ型と SSIS のデータ型](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)」をご覧ください。  
  
###  <a name="use-leading-values"></a><a name="Leading"></a> 先頭の値を使用する  
 シノニムの値ではなく、シノニムのグループの先頭の値が出力されることを指定する場合は、このチェック ボックスをオンにします。 各シノニムの値が正しいフォームまたは修正されたフォームで出力され、そのグループの先頭の値で置き換えられないことを指定する場合は、 **[先頭の値を使用]** をオフにします。  
  
###  <a name="normalize-string"></a><a name="Normalize"></a> 文字列の正規化  
 データ型が **[String]** の場合は、クリックして、DQS によるデータ品質処理のソース データ内の特殊文字を無視します。 データがドメインに読み込まれるときに、DQS によって特殊文字が null またはスペースに内部的に置き換えられます。 コロン、ハイフン、ピリオド、二重引用符、セミコロンはスペースで置き換えられます。 単一引用符は、null で置き換えられます。 null を使用すると、文字列の 2 つの部分を 1 つにまとめることができます。  
  
 文字列値の特殊文字を無視すると、照合の精度が高まります。 特殊文字を null またはスペースで置き換えることで、2 つの文字列間の類似性スコアを上げることができます。 句読点やその他の記号は、別の文字列では異なるものになりがちです。 特殊文字を内部的に置き換えると、スコアが DQS の最小一致しきい値を上回り、2 つの文字列は一致していなくても一致していると見なされます。 ただし、特殊文字を無視するかどうかは、照合を実行しているデータの型によって異なる場合があります。 たとえば、英語の測定系でデータを処理しているときに、二重引用符がインチを表し、単一引用符がフィートを表す場合、製品データの二重引用符と単一引用符を無視すると、結果は偽陽性になります。  
  
 検出、照合ポリシー、照合プロジェクト、クレンジング プロジェクトのアクティビティのデータ処理段階でデータが読み込まれ、インデックス化されるときに、正規化が実行されます。 このプロパティを有効にすると、正規化および用語ベースのリレーションの変換がどちらも分析前の事前処理段階で実行されます。 これらの変換は、文字列間の類似性を計算する任意のアルゴリズムが適用される前に、各ドメインで実行されます。 複合ドメインの解析が要求された場合は、区切り記号の解析に記号が必要なため、正規化および用語ベースのリレーションの変換の前にその解析が実行されます。 ドメイン ルールやドメイン値の変更などの他の操作は変換後に実行されます。 結果データは、DQS の特殊文字の内部的な置換では変更されません。  
  
###  <a name="format-output-to"></a><a name="Format"></a> 形式の出力先  
 ドメイン内のデータ値が出力されるときに適用される書式設定を選択します。 書式設定は、次の一覧に示すように選択されたデータ型に固有です。 **[なし]** を選択すると、リスト内の書式はどれも適用されないことを意味します。  
  
-   文字列値の場合は、出力する文字列を大文字、小文字、または先頭文字のみ大文字として指定できます。  
  
-   日付値の場合は、日、月、および年の形式を指定できます。  
  
-   整数値の場合は、適用される形式マスクの種類を指定できます。  
  
-   10 進数値の場合は、適用される精度と形式マスクの種類を指定できます。  
  
###  <a name="language"></a><a name="Language"></a> 言語  
 データ型が **[String]** の場合は、スペル チェックの操作でドメインに関連付ける言語を選択します。 スペル チェックの結果は使用中の言語に依存するため、この選択項目は、スペル チェックにのみ適用されます。 この選択項目は、データ型が string の単一ドメインにのみ適用されます。 言語プロパティは、複合ドメインとは無関係です。 複合ドメインの各部分の言語は、関連の単一ドメインによって決まります。  
  
 既定の言語は英語です。 **[言語]** プロパティを **[その他]** に設定すると、ドメインのスペル チェックが無効になります。  
  
> [!TIP]  
>  使用している言語が **[言語]** ボックスの一覧に表示されない場合は、 **[その他]** を選択する必要があります。 これにより、ドメインで使用可能なナレッジ (ドメイン ルール、ドメイン値、TBR、照合ルール) に基づいて、一覧に表示されない言語のデータの重複が DQS によってクレンジングおよび排除されます。  
  
###  <a name="enable-speller"></a><a name="Speller"></a> [スペル チェックを有効にする]  
 データ型が **[String]** の場合は、このチェック ボックスをオンにして、ドメインの DQS スペル チェックを有効にします。 スペル チェックは、string データ型のドメインでのみ機能します。 **[スペル チェックを有効にする]** チェック ボックスでは、チェック ボックスに関連付けられている単一ドメインでのみスペル チェックが有効になります。 このチェック ボックスは、複合ドメインには適用されません。  
  
 スペル チェック時に、ドメインの値に対する構文と検証の修正が提案されます。 詳細については、「 [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md)」を参照してください。  
  
###  <a name="disable-syntax-error-algorithms"></a><a name="Syntax"></a> 構文エラーのアルゴリズムを無効にする  
 データ型が **[String]** の場合は、このチェック ボックスをオンにして、クレンジング中にドメイン内の構文エラーが DQS で識別されないことを指定します。 このチェック ボックスは、そのドメインで構文エラーの識別が無関係の場合にオンにします。 たとえば、シリアル番号では構文エラーの識別は重要でない場合があります。 このコントロールは、string データ型でのみ使用できます。 DQS では、string 以外のデータ型について構文エラーはチェックされません。  
  
