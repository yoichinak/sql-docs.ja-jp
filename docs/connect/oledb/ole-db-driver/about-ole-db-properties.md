---
title: OLE DB 接続プロパティについて | Microsoft Docs
description: OLE DB Driver for SQL Server では、コンシューマーがプロパティ値を設定して特定のオブジェクトの動作を要求します。 プロパティの設定について説明します。
ms.custom: ''
ms.date: 05/20/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af733c202d9413cde25abf98974b7bce0ed8284a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727230"
---
# <a name="about-ole-db-properties"></a>OLE DB プロパティについて
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

<!--
NOTE , GeneMi , 2020/May/20:
    This SQL 2016+ article is a nearly exact duplicate of another SQL 2016+ article.
    This article resides under docs/connect/oledb/ole-db-driver/.

    The other article resides under docs/relational-databases/native-client-ole-db-provider/.
    And, the other article has a SQL 2014 counterpart having its same GitHub directory path and filename, to support SQL 2014 OPS Versioning with SQL 2016+.

    This path-file name is:
'\sql-docs-pr\docs\connect\oledb\ole-db-driver\about-ole-db-properties.md'.

    The other path-file is named:
'\sql-docs-pr\docs\relational-databases\native-client-ole-db-provider\about-ole-db-properties.md'.

    Therefore, maybe this docs/connect/oledb/... file should be deleted?

1611957:  This NOTE relates to SEO content bug 1611957 about metadata 'title:' value duplication:
    https://mseng.visualstudio.com/TechnicalContent/_workitems/edit/1611957

PR 15068:  This HTML comment is being added by PR...
    https://github.com/MicrosoftDocs/sql-docs-pr/pull/15068
-->

  コンシューマーは、プロパティ値を設定することで、特定のオブジェクトの動作を要求します。 たとえば、プロパティを使用して、行セットによって公開されるインターフェイスを指定します。 コンシューマーは、プロパティ値を取得して、行セット、セッション、データ ソース オブジェクトなど、オブジェクトの機能を判断します。  
  
 各プロパティには、値、データ型、説明、および読み取り/書き込み属性があります。また、行セット プロパティの場合は、列単位で適用できるかどうかを示すインジケーターがあります。  
  
 プロパティは GUID およびプロパティ ID を表す整数によって識別されます。 プロパティ セットは、同じ GUID を共有するすべてのプロパティのセットです。 OLE DB Driver for SQL Server には、あらかじめ定義されている OLE DB プロパティ セットに加えて、プロバイダー固有のプロパティ セットと、そのセット内のプロパティが実装されています。 各プロパティは、1 つ以上のプロパティ グループに属しています。 プロパティ グループは、特定のオブジェクトに適用されるすべてのプロパティをグループ化したものです。 プロパティ グループには、初期化プロパティ グループ、データ ソース プロパティ グループ、セッション プロパティ グループ、行セット プロパティ グループ、テーブル プロパティ グループ、列プロパティ グループなどがあります。 これらの各プロパティ グループに、プロパティが含まれています。  
  
 プロパティ値を設定するには、次の手順を実行します。  
  
1.  値を設定するプロパティを決定します。  
  
2.  目的のプロパティを含むプロパティ セットを決定します。  
  
3.  目的のプロパティ セットごとに 1 つ、DBPROPSET 構造体の配列を割り当てます。  
  
4.  プロパティ セットごとに DBPROP 構造体の配列を割り当てます。 各配列の要素数は、そのプロパティ セットに属するプロパティ (手順 1. で特定したプロパティ) の個数です。  
  
5.  プロパティごとに DBPROP 構造体に値を設定します。  
  
6.  プロパティ セットごとに DBPROPSET 構造体に情報 (プロパティ セット GUID、要素数、および対応する DBPROP 配列を指すポインター) を設定します。  
  
7.  要素数と DBPROPSET 構造体の配列を渡してメソッドを呼び出し、プロパティを設定します。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のアプリケーションの作成](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [プロパティ [OLE DB]](/previous-versions/windows/desktop/ms722734(v=vs.85))  
  
