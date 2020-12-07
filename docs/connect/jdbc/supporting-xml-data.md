---
description: XML データのサポート
title: XML データのサポート | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da49d5c0468f19768eff720e7f03690bea954432
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396278"
---
# <a name="supporting-xml-data"></a>XML データのサポート
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、XML ドキュメントとフラグメントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納できる **xml** データ型を提供します。 **xml** データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での組み込みデータ型の 1 つであり、**int** や **varchar** などの他の組み込みデータ型といくつかの点で似ています。 他の組み込み型と同様に、**xml** データ型は、テーブルの作成時に列型として使用したり、変数の型やパラメーターの型、関数の戻り値の型として使用したり、[!INCLUDE[tsql](../../includes/tsql-md.md)] の CAST や CONVERT 関数内で使用したりすることができます。 JDBC ドライバーでは、**xml** データ型は、文字列、byte 配列、ストリーム、CLOB、BLOB、または SQLXML オブジェクトとしてマップできます。 文字列が既定のマッピングです。  
  
 この JDBC ドライバーがサポートする JDBC 4.0 API には、SQLXML インターフェイスが導入されています。 SQLXML インターフェイスには、XML データを操作するための各種のメソッドが定義されています。 **SQLXML** は JDBC 4.0 のデータ型であり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** データ型にマップされます。 したがって、アプリケーション内で SQLXML データ型を使用する場合は、sqljdbc4.jar ファイルをインクルードするためのクラスパスを設定する必要があります。 アプリケーションから sqljdbc3.jar を使用して SQLXML オブジェクトやそのメソッドにアクセスしようとすると、例外がスローされます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML データをデータベース列に格納する前に必ず XML データが検証されます。 JDBC ドライバーによって **xml** データ型に自動的にマップされるため、アプリケーションでは **SQLXML** データ型を使用できます。 **SQLXML** のサポートは sqljdbc4.jar に含まれています。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によってサポートされている JRE バージョンの一覧については、「[JDBC Driver のシステム要件](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)」を参照してください。  
  
 このセクションのトピックでは、SQLXML インターフェイスについて説明し、JDBC API のメソッドを使用して **SQLXML** データ型を扱う方法についても説明しています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[SQLXML インターフェイス](../../connect/jdbc/sqlxml-interface.md)|SQLXML のインターフェイスとそのメソッドについて説明します。|  
|[SQLXML でのプログラミング](../../connect/jdbc/programming-with-sqlxml.md)|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API のメソッドを使用し、**SQLXML** Java データ型を介して、リレーショナル データベースに XML データを格納したり、リレーショナル データベースから XML データを取得したりする方法について説明します。 SQLXML オブジェクトの型についての情報や、SQLXML オブジェクトを使用するうえでの重要なガイドラインおよび制限事項の一覧も掲載されています。|  
  
## <a name="see-also"></a>関連項目  
 [JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
