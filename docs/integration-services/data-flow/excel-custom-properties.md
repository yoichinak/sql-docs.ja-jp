---
description: Excel のカスタム プロパティ
title: Excel のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0ad1aa213b09afc77d507b874094122611f96dbf
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123486"
---
# <a name="excel-custom-properties"></a>Excel のカスタム プロパティ

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **変換元のカスタム プロパティ**  
  
 Excel ソースには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、Excel ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|データベースへのアクセスに使用するモード。 値には、 **OpenRowset**、 **OpenRowset from Variable**、 **SQL Command**、および **SQL Command from Variable** があります。 既定値は **OpenRowset** です。|  
|CommandTimeOut|Integer|コマンドのタイムアウトの秒数。値 0 は、タイムアウトしないことを表します。<br /><br /> **注** : このプロパティは、 **Excel ソース エディター** では使用できませんが、 **詳細エディター** を使用して設定できます。|  
|OpenRowset|String|行セットを開くために使用するデータベース オブジェクトの名前。|  
|OpenRowsetVariable|String|行セットを開くために使用するデータベース オブジェクトの名前を格納する変数。|  
|ParameterMapping|String|SQL コマンド内のパラメーターから変数へのマッピング。|  
|SqlCommand|String|実行する SQL コマンド。|  
|SqlCommandVariable|String|実行する SQL コマンドを格納する変数。|  
  
 Excel ソースの出力および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Excel ソース](../../integration-services/data-flow/excel-source.md)」を参照してください。  
  
 **変換先のカスタム プロパティ**  
  
 Excel 変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、Excel 変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|変換先が変換先となるデータベースにアクセスする方法を指定する値。<br /><br /> このプロパティの値は、次のいずれか 1 つです。<br /><br /> **OpenRowset** (0): テーブルまたはビューの名前を指定します。<br /><br /> **OpenRowset from Variable** (1): テーブルまたはビューの名前が含まれる変数の名前を指定します。<br /><br /> **OpenRowset Using Fastload** (3): テーブルまたはビューの名前を指定します。<br /><br /> **OpenRowset Using Fastload from Variable** (4): テーブルまたはビューの名前が含まれる変数の名前を指定します。<br /><br /> **SQL Command** (2): SQL ステートメントを指定します。|  
|CommandTimeOut|Integer|SQL コマンドがタイムアウトになるまでの最大秒数。この値に **0** を指定すると、時間は無制限になります。 このプロパティの既定値は **0** です。<br /><br /> 注: このプロパティは、 **Excel 変換先エディター** では使用できませんが、 **詳細エディター** を使用して設定できます。|  
|FastLoadKeepIdentity|ブール型|データが読み込まれるときに ID 値をコピーするかどうかを指定する値。 このプロパティは、高速読み取りオプションのいずれかを使用した場合のみ使用できます。 このプロパティの既定値は **False** です。|  
|FastLoadKeepNulls|ブール型|データが読み込まれるときに NULL 値をコピーするかどうかを指定する値。 このプロパティは、高速読み取りオプションのいずれかを使用した場合のみ使用できます。 このプロパティの既定値は **False** です。|  
|FastLoadMaxInsertCommitSize|Integer|高速読み込み操作の実行中に、Excel 変換先でコミットを試行するバッチ サイズを指定する値。 既定値は **2147483647** す。 値 **0** は、すべての行が処理された後で、コミット操作が 1 回行われることを示します。|  
|FastLoadOptions|String|高速読み込みオプションのコレクション。 高速読み込みオプションには、テーブルのロックおよび制約のチェックが含まれています。 どちらか 1 つまたは両方を指定することも、どちらも指定しないこともできます。<br /><br /> 注: このプロパティの一部のオプションは、 **[Excel 変換先エディター]** では使用できませんが、 **[詳細エディター]** を使用して設定できます。|  
|OpenRowset|String|AccessMode が **OpenRowset** の場合、Excel 変換先がアクセスするテーブルまたはビューの名前。|  
|OpenRowsetVariable|String|AccessMode が **OpenRowset from Variable** の場合、Excel 変換先がアクセスするテーブルまたはビューの名前が含まれる変数名。|  
|SqlCommand|String|AccessMode が **SQL Command** の場合、Excel 変換先がデータの変換先列を指定するときに使用する、Transact-SQL ステートメント。|  
  
 Excel 変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [Excel 変換先](../../integration-services/data-flow/excel-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
 [SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)
  
