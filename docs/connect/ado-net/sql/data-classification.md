---
title: SqlClient でのデータの検出と分類
description: SQL Server データベースでデータ分類がサポートされているかどうかをチェックする方法、および SqlDataReader オブジェクトを介してデータ分類情報にアクセスする方法について説明します。
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 32c4968c4e734abf7bcb4addfde69bbdc5294d1c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123868"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient でのデータの検出と分類

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[データの検出と分類](../../../relational-databases/security/sql-data-discovery-and-classification.md)は、データベース内の機密データの検出、分類、ラベル付けとレポート作成を行うための高度なサービスのセットです。 SqlClient では、基になるソースが機能をサポートしている場合に、読み取り専用のデータ検出と分類情報を公開する API が提供されています。 この情報には、SqlDataReader を使用してアクセスします。

Microsoft.Data.SqlClient v2.1.0 には、データ分類の `Sensitivity Rank` 情報のサポートが導入されています。 `Sensitivity Rank` は、秘密度ランクを定義する事前に定義された値のセットに基づく識別子です。 ランクに基づいて異常を検出するため、Advanced Threat Protection などの他のサービスによって使用できます。 次の Data Classification API を、Microsoft.Data.SqlClient.DataClassification 名前空間で利用できるようになりました。

```csharp
// New in Microsoft.Data.SqlClient v2.1.0
public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}

public sealed class SensitivityClassification
{
  // Returns the sensitivity rank for the query associated with the active 'SqlDataReader'.
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the labels collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<Label> Labels;

  // Returns the information types collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<InformationType> InformationTypes;

  // Returns the column sensitivity for this 'SensitivityClassification' Object
  public ReadOnlyCollection<ColumnSensitivity> ColumnSensitivities;
}

public sealed class SensitivityProperty
{
  // Returns the sensitivity rank for this 'SensitivityProperty' Object
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the label for this 'SensitivityProperty' Object
  public Label Label;

  // Returns the information type for this 'SensitivityProperty' Object
  public InformationType InformationType;
}

public sealed class Label
{
  // Gets the name for this 'Label' object
  public string Name;

  // Gets the ID for this 'Label' object
  public string Id;
}

public sealed class InformationType
{
  // Gets the name for this 'InformationType' object
  public string Name;

  // Gets the ID for this 'InformationType' object
  public string Id;
}

public sealed class ColumnSensitivity
{
  // Returns the list of sensitivity properties as received from Server for this 'ColumnSensitivity' information      
  public ReadOnlyCollection<SensitivityProperty> SensitivityProperties;
}
```

> [!NOTE]
> ランクを含むデータ分類が SQL Server でサポートされている場合にのみ、Microsoft.Data.SqlClient によって `Sensitivity Rank` の情報が読み取られます。 サーバーでランクのない古いバージョンのデータ分類が使用されている場合、クエリでのランクの値は "未定義" になります。

このサンプル アプリケーションは、SqlDataReader のデータ分類プロパティにアクセスする方法を示しています。

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]


**参照**  

 - [SQL Server の機能と ADO.NET](sql-server-features-adonet.md)
 - [sys.sensitivity_classifications (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
 - [ADD SENSITIVITY CLASSIFICATION](../../../t-sql/statements/add-sensitivity-classification-transact-sql.md)