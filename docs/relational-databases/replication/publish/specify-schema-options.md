---
description: SQL Server レプリケーションのスキーマ オプションを指定する
title: SQL Server レプリケーションのスキーマ オプションを指定する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2f160e1c9014e6b54590c50726c9b3bbae0e64f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88405888"
---
# <a name="specify-schema-options-for-sql-server-replication"></a>SQL Server レプリケーションのスキーマ オプションを指定する
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、スキーマのオプションを指定する方法について説明します。 テーブルまたはビューをパブリッシュするとき、パブリッシュされたオブジェクト用にレプリケートされるオブジェクトの作成オプションを制御できます。 アーティクルが作成されるときにこれらのオプションを設定することができ、後で変更することもできます。 アーティクルに対してオプションを明示的に指定しなかった場合、既定のオプションが定義されます。  
  
> [!NOTE]  
>  レプリケーションのストアド プロシージャを使用した場合の既定のスキーマ オプションは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使ってアーティクルを追加するときの既定のオプションとは異なる場合があります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
-   **スキーマ オプションを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションの作成後にスキーマ オプションを変更する場合は、新しいスナップショットを生成する必要があります。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   すべてのスキーマ オプションの一覧については、「[sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」および「[sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」の `@schema_option` パラメーターをご覧ください。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 スキーマ オプション (制約やトリガーをサブスクライバーにコピーするかどうかなど) は、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブで指定します。 このタブは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-specify-schema-options"></a>スキーマ オプションを指定するには  
  
1.  パブリケーションの新規作成ウィザードまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、アーティクルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  スキーマ オプションの変更を適用するアーティクルを選択します。  
  
    -   **[反転表示された \<ObjectType> アーティクルのプロパティを設定]** をクリックして、 **[アーティクルのプロパティ - \<ObjectName>]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、 **[アーティクル]** ページのオブジェクト ペインで反転表示されたオブジェクトのみに適用されます。  
  
    -   **[すべての\<ObjectType> アーティクルのプロパティを設定]** をクリックして、 **[すべての \<ObjectType> アーティクルのプロパティ]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、パブリケーション用に選択されていないオブジェクトも含め、 **[アーティクル]** ページのオブジェクト ペインにあるこの種類のすべてのオブジェクトに適用されます。  
  
        > [!NOTE]  
        >  **[すべての \<ObjectType> アーティクルのプロパティ]** ダイアログ ボックスで行われたプロパティの変更は、 **[アーティクルのプロパティ - \<ObjectName>]** ダイアログ ボックスで以前行われた変更をすべてオーバーライドします。 たとえば、あるオブジェクトの種類のすべてのアーティクルに対して複数の既定を設定し、かつそれぞれのオブジェクトに対してプロパティを設定する場合には、最初にすべてのアーティクルに対する既定を設定します。 次に、それぞれのオブジェクトに対してプロパティを設定します。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[サブスクライバーへのオブジェクトと設定のコピー]** および **[対象オブジェクト]** セクションで、オプションの値を設定します。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 スキーマ オプションは、1 つまたは複数のオプションについて、 [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) を実行した結果を 16 進数値で指定します。 詳細については、「 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 」および「 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  ビットごとの演算を実行する際は、あらかじめ、スキーマ オプションの値を **binary** から **int** に変換しておく必要があります。 詳細については、「[CAST and CONVERT &#40;Transact-SQL&#41;](../../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前、`@article` にアーティクル名、`@source_object` にパブリッシュするデータベース オブジェクト、`@type` にデータベース オブジェクトの型を指定し、さらに、1 つまたは複数のスキーマ オプションに対する [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) の結果を `@schema_option` に指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>マージ パブリケーションのアーティクルを定義するときにスキーマ オプションを指定するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前、`@article` にアーティクル名、`@source_object` にパブリッシュするデータベース オブジェクトを指定し、さらに、1 つまたは複数のスキーマ オプションに対する [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) の結果を `@schema_option` に指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの既存のアーティクルに設定されているスキーマ オプションを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)を実行します。 `@publication` と `@article` に、それぞれアーティクルが属しているパブリケーションの名前およびアーティクル名を指定します。 結果セットの `schema_option` 列の値を確認します。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 演算を実行します。  
  
4.  パブリッシャーのパブリケーション データベースで [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前を、`@article` にアーティクル名を、`@property` の値に `schema_option` を指定し、さらに、手順 3 で得られた 16 進数値を `@value` に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>マージ パブリケーションの既存のアーティクルのスキーマ オプションを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)を実行します。 `@publication` と `@article` に、それぞれアーティクルが属しているパブリケーションの名前およびアーティクル名を指定します。 結果セットの **schema_option** 列の値を確認してください。  
  
2.  手順 1 の値、および必要なスキーマ オプションの値を使って [& (ビット演算 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 演算を実行し、対象のオプションが設定されているかどうかを確認します。  
  
    -   実行結果が **0**の場合、オプションは設定されていません。  
  
    -   実行結果がオプションの値の場合、そのオプションは既に設定されています。  
  
3.  オプションが設定されていなかった場合は、手順 1. の値と、必要なスキーマ オプション値を使って [| (ビット演算 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 演算を実行します。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)を実行します。 `@publication` にアーティクルが属しているパブリケーションの名前を、`@article` にアーティクル名を、`@property` の値に `schema_option` を指定し、さらに、手順 3 で得られた 16 進数値を `@value` に指定します。  
  
5.  スナップショット エージェントを実行して、新しいスナップショットを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
