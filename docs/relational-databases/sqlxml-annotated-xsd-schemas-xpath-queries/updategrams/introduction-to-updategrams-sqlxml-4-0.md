---
title: アップデートグラムの概要 (SQLXML)
description: データベース内のデータの挿入、更新、または削除に使用できる SQLXML 4.0 アップデートグラムについて説明します。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6a416950247208c682d0fdc923db71357405fd0e
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98170624"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>アップデートグラムの概要 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アップデートグラムまたは OPENXML 関数を使用して、既存の XML ドキュメントからデータベースを変更 (挿入、更新、または削除) することができ [!INCLUDE[tsql](../../../includes/tsql-md.md)] ます。  
  
 OPENXML 関数は、既存の XML ドキュメントを断片化し、INSERT、UPDATE または DELETE ステートメントに渡すことができる行セットを提供することで、データベースを変更する関数です。 OPENXML を使用すると、データベース テーブルに対して操作を直接実行できます。 したがって、ソースにテーブルなどの行セット プロバイダーがある場合は常に、OPENXML を使用するのが最適です。  
  
 アップデートグラムを使用すると、OPENXML と同様にデータベースに対してデータを挿入、更新、または削除できます。ただし、アップデートグラムは注釈付き XSD (または XDR) スキーマにより提供される XML ビューに対して動作します。たとえば、更新はマッピング スキーマにより提供される XML ビューに適用されます。 マッピング スキーマには、XML 要素と属性を対応するデータベース テーブルと列にマップするための、必要な情報が含まれています。 アップデートグラムでは、このマッピング情報を使用してデータベース テーブルと列が更新されます。  
  
> [!NOTE]  
>  このドキュメントは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされるテンプレートとマッピング スキーマについて理解していることを前提としています。 詳細については、「 [注釈付き XSD スキーマの概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)」を参照してください。 XDR を使用するレガシアプリケーションでは、 [SQLXML 4.0&#41;では、注釈付き Xdr スキーマ &#40;非推奨 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)とされています。  
  
## <a name="required-namespaces-in-the-updategram"></a>アップデートグラムで必要な名前空間  
 、、およびなどのアップデートグラムのキーワードは、 **\<sync>** **\<before>** **\<after>** **urn: schema-microsoft-com: xml アップデートグラム** の名前空間にあります。 名前空間プレフィックスは、任意のものを使用できます。 このドキュメントでは、 **updg** プレフィックスは **アップデートグラム** の名前空間を示しています。  
  
## <a name="reviewing-syntax"></a>構文の確認  
 アップデートグラムは、、、およびの各ブロックを含むテンプレートで、 **\<sync>** **\<before>** **\<after>** アップデートグラムの構文を形成します。 次のコードは、最も単純な構文です。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 次に、これらの各ブロックの役割について説明します。  
  
 **\<before>**  
 レコード インスタンスの既存の状態 ("before 状態") を指定します。  
  
 **\<after>**  
 データの変更後の新しい状態を指定します。  
  
 **\<sync>**  
 とブロックを格納し **\<before>** **\<after>** ます。 **\<sync>** ブロックには、およびブロックのセットを複数含めることができ **\<before>** **\<after>** ます。 ブロックとブロックのセットが複数ある場合は **\<before>** **\<after>** 、これらのブロック (空の場合でも) をペアとして指定する必要があります。 さらに、アップデートグラムには複数のブロックを含めることができ **\<sync>** ます。 各 **\<sync>** ブロックは1つのトランザクション単位です (つまり、ブロック内のすべての処理が完了しているか、何も実行されていないことを意味 **\<sync>** します)。 アップデートグラムに複数のブロックを指定した場合 **\<sync>** 、1つのブロックでエラーが発生しても、他のブロックには **\<sync>** 影響しません **\<sync>** 。  
  
 アップデートグラムでレコードインスタンスを削除、挿入、または更新するかどうかは、ブロックとブロックの内容によって異なり **\<before>** **\<after>** ます。  
  
-   レコードインスタンスがブロック内にのみ存在し、 **\<before>** 対応するインスタンスがブロック内に存在しない場合 **\<after>** 、アップデートグラムは削除操作を実行します。  
  
-   レコードインスタンスがブロック内にのみ存在し、 **\<after>** 対応するインスタンスがブロック内に存在しない場合 **\<before>** は、挿入操作になります。  
  
-   レコードインスタンスがブロック内に存在 **\<before>** し、対応するインスタンスがブロック内にある場合 **\<after>** は、更新操作です。 この場合、アップデートグラムでは、レコードインスタンスがブロックに指定されている値に更新され **\<after>** ます。  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>アップデートグラムでマッピングスキーマを指定する  
 アップデートグラムでは、暗黙的または明示的に、マッピング スキーマによって XML データを操作できます。つまり、マッピング スキーマを指定しても指定しなくてもアップデートグラムは動作します。マッピング スキーマは XSD と XDR の両方がサポートされています。 マッピングスキーマを指定しない場合、アップデートグラムでは、暗黙的なマッピング (既定のマッピング) が使用されます。このマッピングでは、ブロックまたはブロック内の各要素が **\<before>** **\<after>** テーブルにマップされ、各要素の子要素または属性がデータベース内の列にマップされます。 マッピング スキーマを明示的に指定する場合、アップデートグラムの要素と属性は、マッピング スキーマ内の要素と属性に一致する必要があります。  
  
### <a name="implicit-default-mapping"></a>暗黙的なマッピング (既定)  
 単純な更新を実行するアップデートグラムではほとんどの場合、マッピング スキーマは必要ありません。 この場合、アップデートグラムは既定のマッピング スキーマに従います。  
  
 次のアップデート グラムは、暗黙的なマッピングを示しています。 この例では、アップデートグラムによって新しい顧客が Sales.Customer テーブルに挿入されます。 このアップデートグラムでは暗黙的なマッピングが使用されるため、 \<Sales.Customer> 要素は sales. customer テーブルにマップされ、CustomerID 属性と SalesPersonID 属性が sales. customer テーブル内の対応する列にマップされます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>明示的なマッピング  
 XSD または XDR のいずれかのマッピング スキーマを指定した場合、アップデートグラムではそのスキーマによって、更新するデータベース テーブルと列が決定されます。  
  
 アップデートグラムで複雑な更新を実行する場合 (マッピングスキーマで指定されている親子リレーションシップに基づいて複数のテーブルにレコードを挿入する場合など) は、アップデートグラムを実行する **マッピング** スキーマ属性を使用してマッピングスキーマを明示的に指定する必要があります。  
  
 アップデートグラムはテンプレートであり、アップデートグラム内でマッピング スキーマに指定するパスは、テンプレート ファイルの場所 (アップデートグラムが保存されている場所) に対する相対パスです。 詳細については、「 [アップデートグラムでの注釈付きマッピングスキーマの指定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)」を参照してください。  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>アップデートグラムでの要素中心および属性中心のマッピング  
 アップデートグラムでマッピング スキーマが指定されていないときに使用される既定のマッピングでは、アップデートグラムの要素がテーブルにマップされ、要素中心マッピングの場合は子要素、属性中心マッピングの場合は属性が、それぞれ列にマップされます。  
  
### <a name="element-centric-mapping"></a>要素中心のマッピング  
 要素中心のアップデートグラムでは、要素に、要素のプロパティを表す子要素を含めます。 たとえば、次のアップデートグラムを参照してください。 **\<Person.Contact>** 要素には、 **\<FirstName>** **\<LastName>** 子要素と子要素が含まれています。 これらの子要素は、要素のプロパティです **\<Person.Contact>** 。  
  
 このアップデートグラムではマッピングスキーマが指定されていないため、このアップデートグラムでは暗黙的なマッピングを使用します。この場合、 **\<Person.Contact>** 要素は Person テーブルとその子要素にマップされ、FirstName 列と LastName 列にマップされます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>属性中心のマッピング  
 属性中心のマッピングでは、要素に属性を指定します。 たとえば、次のアップデートグラムでは属性中心のマッピングが使用されています。 この例では、 **\<Person.Contact>** 要素は **FirstName** 属性と **LastName** 属性で構成されています。 これらの属性は、要素のプロパティ **\<Person.Contact>** です。 前の例と同様に、このアップデートグラムではマッピングスキーマが指定されていないため、 **\<Person.Contact>** 要素を Person. Contact テーブルにマップし、要素の属性をテーブル内のそれぞれの列にマップするために、暗黙的なマッピングに依存しています。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>要素中心と属性中心の両方のマッピングの使用  
 次のアップデートグラムに示すように、要素中心と属性中心のマッピングは併用できます。 要素には **\<Person.Contact>** 属性と子要素の両方が含まれていることに注意してください。 また、このアップデートグラムは暗黙的なマッピングに従います。 このため、 **FirstName** 属性と **\<LastName>** child 要素は、Person. Contact テーブルの対応する列にマップされます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>SQL Server で有効であり、XML で有効でない文字の取り扱い  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、テーブル名に空白を含めることができます。 ただし、このようなテーブル名は XML では有効でありません。  
  
 有効な識別子であるが有効な XML 識別子ではない文字をエンコードするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \_ \_ エンコード値として ' __xHHHH ' を使用します。ここで、HHHH は、最上位ビットから順に、文字の4桁の16進数の UCS 2 コードを表します。 このエンコード方式を使用すると、スペース文字は x0020 (スペース文字の4桁の16進コード) に置き換えられます。このため、のテーブル名 [Order Details] は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML で _x005B_Order_x0020_Details_x005D になり \_ ます。  
  
 同様に、などの3つの要素で構成される要素名を指定する必要がある場合もあり \<[database].[owner].[table]> ます。 角かっこ文字 ([および]) は XML では無効であるため、これをとして指定する必要があります \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_> \_ 。 _x005B は左角かっこ ([) のエンコーディングで、_x005D \_ は右角かっこ (]) のエンコーディングです。  
  
## <a name="executing-updategrams"></a>アップデートグラムの実行  
 アップデートグラムはテンプレートであり、テンプレートのすべての処理メカニズムが適用されます。 SQLXML 4.0 では、アップデートグラムを次のいずれかの方法で実行できます。  
  
-   ADO コマンドに含めて送信する。  
  
-   OLE DB コマンドとして送信する。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
