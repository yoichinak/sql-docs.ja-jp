---
description: Azure Data Lake Store Source
title: Azure Data Lake Store Source | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38de021617ed0454048a3d8cd7f0c5732d09861f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127337"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store Source

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Azure Data Lake Store Source** コンポーネントは、SSIS パッケージが Azure Data Lake Store からデータを読み取れるようにします。 サポートされるファイル形式は、テキストと Avro です。
  
 **Azure Data Lake Store Source** は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。  
  
> [!NOTE]
> Azure Data Lake Store 接続マネージャーとこれを使用するコンポーネント (つまり、Azure Data Lake Store Source と Azure Data Lake Store Destination) がサービスに接続できるようにするために、必ず最新バージョンの Azure Feature Pack を [こちら](https://www.microsoft.com/download/details.aspx?id=49492)からダウンロードしてください。 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Azure Data Lake Store Source を構成する
 1. Azure Data Lake Store のエディターを表示するには、データ フロー デザイナー上に **Azure Data Lake Store Source** をドラッグ アンド ドロップし、これをダブルクリックしてエディターを開きます。  
  
2.  **[Azure Data Lake Store connection manager (Azure Data Lake Store 接続マネージャー)]** フィールドに、既存の Azure Data Lake Store 接続マネージャーを指定するか、Azure Data Lake Store サービスを参照する新しいものを作成します。  
  
    1.  **[ファイル パス]** フィールドには、Azure Data Lake Store のソース ファイルのファイル パスを指定します。   
  
    2.  **[ファイル形式]** フィールドには、ソース ファイルのファイル形式を指定します。  
  
        テキスト ファイル形式の場合は、 **[列の区切り文字]** に値を指定する必要があります。 さらに、ファイルの 1 行目に列名が含まれている場合は、 **[先頭データ行を列名として使用する]** も指定する必要があります。  
  
3.  接続情報を指定した後、 **[列]** ページで、SSIS データ フローのマップ元の列をマップ先の列にマップします。   

## <a name="text-qualifier"></a>テキスト修飾子

**Azure Data Lake Store Source** はテキスト修飾子をサポートしません。 ファイルを正しく処理するためにテキスト修飾子を指定する必要がある場合、ファイルをローカル コンピューターにダウンロードし、**フラット ファイル ソース** を使用してファイルを処理することを検討してください。 フラット ファイル ソースでテキスト修飾子を指定できるようになります。 詳細については、「[フラット ファイル ソース](flat-file-source.md)」を参照してください。
