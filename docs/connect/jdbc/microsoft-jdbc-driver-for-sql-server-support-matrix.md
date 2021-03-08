---
title: Microsoft SQL Server 用 JDBC Driver のサポート表
description: このページには、Microsoft JDBC Driver for SQL Server のサポート表とサポート ライフサイクル ポリシーがあります。
ms.custom: ''
ms.date: 02/26/2021
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fb84ce512cca3e87f0ec108698928caa2934122
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101835362"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Microsoft SQL Server 用 JDBC Driver のサポート表

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  このページには、Microsoft SQL Server 用 JDBC Driver のサポート表とサポート ライフサイクル ポリシーがあります。  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Microsoft JDBC Driver サポート ライフサイクルの表とポリシー  

マイクロソフト サポート ライフサイクル (MSL) ポリシーでは、マイクロソフト製品のサポート ライフサイクルを理解しやすくする、予測可能な情報を提供しています。 JDBC ドライバーのバージョン 4.x、6.x、7.x、8.x、9.x には、ドライバーのリリース日から 5 年間のメインストリーム サポートが含まれています。 メインストリーム サポートについては、Microsoft ライフサイクル ポリシーの Web サイトで定義されています。  
  
延長サポートとカスタム サポートのオプションは、Microsoft JDBC Driver では使用できません。  

次の Microsoft JDBC Driver は、表示されているサポートの終了日までサポートされます。  
  
|ドライバー名|ドライバー パッケージのバージョン|適用できる JAR|メインストリーム サポートの終了|
|-|-|-|-|  
|Microsoft JDBC Driver 9.2 for SQL Server|9.2|mssql-jdbc-9.2.1.jre15.jar<br> mssql-jdbc-9.2.1.jre11.jar<br> mssql-jdbc-9.2.1.jre8.jar|2026 年 1 月 29 日|
|Microsoft JDBC Driver 8.4 for SQL Server|8.4|mssql-jdbc-8.4.1.jre14.jar<br> mssql-jdbc-8.4.1.jre11.jar<br> mssql-jdbc-8.4.1.jre8.jar|2025 年 7 月 31 日|
|Microsoft JDBC Driver 8.2 for SQL Server|8.2|mssql-jdbc-8.2.2.jre13.jar<br> mssql-jdbc-8.2.2.jre11.jar<br> mssql-jdbc-8.2.2.jre8.jar|2025 年 1 月 31 日|
|Microsoft JDBC Driver 7.4 for SQL Server|7.4|mssql-jdbc-7.4.1.jre12.jar<br> mssql-jdbc-7.4.1.jre11.jar<br> mssql-jdbc-7.4.1.jre8.jar|2024 年 7 月 31 日|
|Microsoft JDBC Driver 7.2 for SQL Server|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|2024 年 1 月 31 日|
|Microsoft JDBC Driver 7.0 for SQL Server|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|2023 年 7 月 31 日|
|Microsoft SQL Server 用 JDBC Driver 6.4|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|2023 年 2 月 27 日|
|Microsoft JDBC Driver 6.2 for SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|2022 年 6 月 30 日|
|Microsoft SQL Server 用 JDBC Driver 6.0|6.0|sqljdbc42.jar<br>sqljdbc41.jar|2021 年 7 月 14 日|
  
 次の Microsoft JDBC ドライバーはサポートされなくなりました。  

|ドライバー名|ドライバー パッケージのバージョン|メインストリーム サポートの終了|  
|-|-|-|
|Microsoft SQL Server 用 JDBC Driver 4.2|4.2|2020 年 8 月 24 日|
|Microsoft SQL Server 用 JDBC Driver 4.1|4.1|2019 年 12 月 12日|  
|Microsoft SQL Server 用 JDBC Driver 4.0|4.0|2017 年 3 月 6 日|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|2015 年 4 月 23 日|  
|Microsoft SQL Server JDBC Driver 2.0|2.0|2012 年 12 月 31 日|  
|Microsoft SQL Server 2005 JDBC ドライバー 1.2|1.2|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.1|1.1|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.0|1.0|2011 年 6 月 25 日|  
|Microsoft SQL Server 2000 JDBC Driver|2000|2010 年 7 月 9 日|  
  
## <a name="sql-version-compatibility"></a>SQL バージョンの互換性  
  
|データベースのバージョン&nbsp;&#8594;<br />&#8595; ドライバーのバージョン|Azure SQL データベース|Azure Synapse Analytics|Azure SQL Managed Instance|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2008 R2|SQL Server 2008|
|---|---|---|---|---|---|---|---|---|---|---|---|
|9.2|はい|はい|はい|はい|はい|はい|はい|はい|   |   |   |
|8.4|はい|はい|はい|はい|はい|はい|はい|はい|はい|   |   |
|8.2|はい|はい|はい|はい|はい|はい|はい|はい|はい|   |   |
|7.4|はい|はい|はい|はい|はい|はい|はい|はい|はい|   |   |
|7.2|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|7.0|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|6.4|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|6.2|はい|はい|   |   |はい|はい|はい|はい|はい|はい|はい|
|6.1|はい|   |   |   |   |はい|はい|はい|はい|はい|はい|
|6.0|はい|   |   |   |   |はい|はい|はい|はい|はい|はい|
|4.2|はい|   |   |   |   |はい|はい|はい|はい|はい|はい|
|4.1|はい|   |   |   |   |はい|はい|はい|はい|はい|はい|
|4.0|はい|   |   |   |   |はい|はい|はい|はい|はい|はい|
|3.0|はい<sup>2</sup>|   |   |   |   |   |○<sup>5</sup>|可<sup>1</sup>|   |はい|はい|
|2.0|   |   |   |   |   |   |   |   |   |○<sup>3</sup>|○<sup>3</sup>|
|1.2|   |   |   |   |   |   |   |   |   |   |○<sup>3</sup>|

 <sup>1</sup>Microsoft SQL Server JDBC Driver バージョン 3.0 では、下位クライアントの SQL Server 2012 に接続できます。  
  
 <sup>2</sup>3.0 のドライバーには、修正プログラムとして Azure SQL Database のサポートが導入されています。 Azure SQL Database のお客様は、最新バージョンのドライバーを使用することをおすすめします。  
  
 <sup>3</sup>Microsoft SQL Server JDBC Driver バージョン 2.0 と Microsoft SQL Server 2005 JDBC Driver バージョン 1.2 では、下位クライアントの SQL Server 2008 に接続できます。 下位変換が許可されている場合、アプリケーションはクエリを実行し、新しい SQL Server 2008 データ型 (time、date、datetime2、datetimeoffset、FILESTREAM など) の更新を実行できます。 これらの新しいデータ型を JDBC ドライバーで使用する方法の詳細については、「  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver (JDBC ドライバーを使用して SQL Server 2008 の日付/時刻データ型を操作する)](/archive/blogs/jdbcteam/) 」および「  [Working with SQL Server 2008 FileStream using JDBC Driver (JDBC ドライバーを使用して SQL Server 2008 の FileStream を操作する](/archive/blogs/jdbcteam/)」をご覧ください。 これらの新しいデータ型の下位互換性の詳細については、SQL Server オンライン ブックの「  [日時データの使用](/previous-versions/sql/sql-server-2008-r2/ms180878(v=sql.105))」および「  [FILESTREAM のサポート](../../relational-databases/native-client/features/filestream-support.md) 」トピックをご覧ください。  
  
 <sup>4</sup>Microsoft JDBC Driver と並列データ ウェアハウス間の接続のサポートが、Microsoft JDBC Driver 4.0 for SQL Server と Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance Update 3 で初めて導入されました。  
  
 <sup>5</sup>Microsoft SQL Server JDBC Driver バージョン 3.0 では、下位クライアントの SQL Server 2014 に接続できます。  
  
## <a name="java-and-jdbc-specification-support"></a>Java と JDBC の仕様のサポート
  
|JDBC ドライバーのバージョン|JRE のバージョン|JDBC API のバージョン|
|-|-|-|
|[9.2](release-notes-for-the-jdbc-driver.md#92)|1.8、11、15|4.2、4.3 (部分)|
|[8.4](release-notes-for-the-jdbc-driver.md#84)|1.8、11、14|4.2、4.3 (部分)|
|[8.2](release-notes-for-the-jdbc-driver.md#82)|1.8、11、13|4.2、4.3 (部分)|
|[7.4](release-notes-for-the-jdbc-driver.md#74)|1.8、11、12|4.2、4.3 (部分)|
|[7.2](release-notes-for-the-jdbc-driver.md#72)|1.8、11|4.2、4.3 (部分)|
|[7.0](release-notes-for-the-jdbc-driver.md#70)|1.8、10|4.2、4.3 (部分)|
|[6.4](release-notes-for-the-jdbc-driver.md#64)|1.7、1.8、9|4.1、4.2、4.3 (部分)|
|[6.2](release-notes-for-the-jdbc-driver.md#62)|1.7、1.8|4.1、4.2|
|[6.1](release-notes-for-the-jdbc-driver.md#61)|1.7、1.8|4.1、4.2|
|[6.0](release-notes-for-the-jdbc-driver.md#60)|1.7、1.8|4.1、4.2|
|4.2|1.7、1.8|4.1、4.2|
|4.1|1.7|4.0|
|4.0|1.5, 1.6, 1.7|3.0, 4.0|
|3.0|1.5, 1.6,|3.0, 4.0|
|2.0|1.5, 1.6|3.0, 4.0|
|1.2|1.4, 1.5, 1.6|3.0|
|1.1|1.4|3.0|
|1.0|1.4|3.0|
|2000|1.4|3.0|

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

Microsoft JDBC Driver は、Java 仮想マシン (JVM) の使用をサポートするすべてのオペレーティング システムで機能するように設計されています。 一般的に使用されるプラットフォームには、Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 R2、Linux、Unix、AIX、macOS などがあります。  

JDBC 製品チームは、Windows、Sun Solaris、SUSE Linux、Ubuntu Linux、CentOS Linux、および macOS でドライバーをテストしています。

## <a name="application-server-support"></a>アプリケーション サーバーのサポート

Microsoft SQL Server 用 JDBC Driver は、さまざまなアプリケーション サーバーでテストされています。  これらの製品と互換性のあるドライバー バージョンの詳細情報については、ご利用のアプリケーション サーバーの製造元にお問い合わせください。