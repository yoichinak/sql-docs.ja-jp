---
description: SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング
title: SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 946bb57a3d821186ebcca132539713cf515ab20f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122817"
---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、列の名前、データ型、およびデータ型プロパティを新しい変換先テーブルとファイルに設定できますが、列の値についてカスタム変換を指定することはできません。 このため、変換元から変換先へのデータ型の組み込みマッピングが重要になります。  
  
##  <a name="how-does-the-wizard-map-data-types-between-source-and-destination"></a><a name="wizardMapping"></a> ウィザードが変換元と変換先の間でデータ型をマップする方法
ウィザードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によってインストールされたマッピング ファイルを使用して、データベース システムまたはバージョン間でデータ型がマップされます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型から Oracle データ型にマップできます。 既定では、XML 形式のマッピング ファイルは次のフォルダにインストールされます。
-   **C:\Program Files\Microsoft SQL Server\130\DTSMappingFiles\\** (64 ビットの場合)
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTSMappingFiles\\** (32 ビットの場合)。  
  
 既存のマッピング ファイルを編集した、または新しいマッピング ファイルをフォルダーに追加した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードまたは [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を終了してから再度開いて、新しいファイルまたは更新したファイルを読み込む必要があります。  
 
## <a name="you-can-change-an-existing-mapping-file"></a>既存のマッピング ファイルを変更できる
既定と異なるデータ型のマッピングが必要な場合は、マッピング ファイルを更新して、ウィザードによって使用されるマッピングを変更できます。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から DB2 にデータを転送するときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** データ型を DB2 **VARGRAPHIC** データ型ではなく DB2 **GRAPHIC** データ型にマップするには、 **SqlClientToIBMDB2.xml** マッピング ファイルで **nchar** マッピングを変更して、**VARGRAPHIC.** ではなく **GRAPHIC** を使用します。  
  
## <a name="you-can-add-a-new-mapping-file"></a>新しいマッピング ファイルを追加できる
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、一般的な変換元と変換先の組み合わせのマッピングをインストールします。 他の変換元と変換先の組み合わせをサポートする新しいマッピング ファイルを **MappingFiles** ディレクトリに追加することもできます。 新しいマッピング ファイルは、公開されている XSD スキーマおよび変換元と変換先の一意の組み合わせ間でのマッピングに準拠する必要があります。 マッピング ファイルのスキーマである **DataTypeMapping.xsd** は、 [こちら](https://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd)に公開されています。
 
## <a name="sample-mapping-file"></a>サンプル マッピング ファイル
次に示すのは、SQL Server データ型 (具体的には .Net Framework Data Provider for SQL Server で使用されるデータ型) から Oracle データ型にマップする XML マッピングファイルの一部です。 一例として、SQL Server の **int** データ型が Oracle の **INTEGER** データ型にマップされることを確認できます。
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="https://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  

