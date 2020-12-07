---
title: CLR ルーチンのカスタム属性 |Microsoft Docs
description: カスタム属性は、CLR ルーチン、ユーザー定義型、および Microsoft SQL Server に登録されているユーザー定義集計に適用できます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810808"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR ルーチン用の CLR 統合のカスタム属性
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  ここに示されている属性は、に登録されている共通言語ランタイム (CLR) ルーチン、ユーザー定義型、およびユーザー定義集計に適用でき [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。 属性が適用されない場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は既定値を想定します。 一覧表示される属性は、 **Microsoft の SqlServer** 名前空間で定義されています。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 属性  
 **Sqluserdefinedaggregate**属性は、メソッドをユーザー定義集計として登録する必要があることを示します。 すべてのユーザー定義集計にこのカスタム属性で注釈を付ける必要があります。  
  
 詳細については、「 [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute)」を参照してください。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 属性  
 **Sqlfunction**属性は、適切な関数属性が設定されたメソッドを関数として登録する必要があることを示します。  
  
 詳細については、「 [Sqlfunctionattribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute)」を参照してください。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 属性  
 **Sqlfacet**属性は、ユーザー定義型 (UDT) 式の戻り値の型に関する情報を返すために使用されます。  
  
 詳細については、「 [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute)」を参照してください。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 属性  
 **Sqlprocedure**属性は、メソッドをストアドプロシージャとして登録する必要があることを示します。 この属性は、Visual Studio だけで使用され、指定されたメソッドがストアド プロシージャとして自動的に登録されます。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では使用されません。  
  
 詳細については、「 [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute)」を参照してください。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 属性  
 **Sqltrigger**属性は、メソッドをトリガーとして登録する必要があることを示します。  
  
 詳細については、「 [Sqltriggercontext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) 」と「 [sqltriggercontext](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute)」を参照してください。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 SqlUserDefinedTypeAttribute をアセンブリのクラス定義に適用できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、これにより、このカスタム属性を持つクラス定義にバインドされたユーザー定義型が作成されます。  
  
 詳細については、「 [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute)」を参照してください。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 属性  
 **Sqlmethod**属性は、UDT のメソッドまたはプロパティの決定性およびデータアクセスプロパティを示すために使用されます。  
  
 詳細については、「 [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CLR ユーザー定義集計](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR ユーザー定義関数](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR ユーザー定義型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR ストアドプロシージャ](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [CLR トリガー](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
