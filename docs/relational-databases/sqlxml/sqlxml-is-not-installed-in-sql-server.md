---
description: SQL Server で SQLXML がインストールされない
title: SQL Server で SQLXML がインストールされない
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c0fee1b0ad59aa8a07e8f95decd94e84c6af225
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490370"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQL Server で SQLXML がインストールされない
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のバージョンでは、SQLXML 4.0 は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属してリリースされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのバージョン ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] を除く) の既定のインストールに含まれていました。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、SQLXML の最新バージョン (SQLXML 4.0 SP1) が含まれないようになりました。 SQLXML 4.0 SP1 をインストールするには、 [sqlxml 4.0 sp1 のインストール場所](https://www.microsoft.com/download/details.aspx?id=30403)からダウンロードします。  
  
 アプリケーションがで実行さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れ、sqlxml 4.0 が必要な場合は、sqlxml 4.0 SP1 をダウンロードしてインストールする必要があります。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB および SQL Server Native Client OLE DB プロバイダーを使用した場合の新しいデータ型による SQLXML 4.0 SP1 の動作  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では次のデータ型が導入されました。 SQLXML を使用する開発者は、を使用することをお勧めします。  
  
-   **日付**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 SQLOLEDB または Native Client OLE DB のいずれかを使用して SQLXML 4.0 SP1 を使用する場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 、これらの型は開発者に文字列として表示されます。 SQLXML 4.0 SP1 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 以降で使用する場合に、これら4つの新しいデータ型を組み込みスカラー型として有効にします。 SQLXML 4.0 SP1 をダウンロードしないと、これらの型を文字列以外の型にマッピングした場合、一部のデータが切り捨てられる可能性があります。 たとえば、 **DateTime2** を **xsd: date** にマッピングすると、データは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 3.33 ミリ秒の **DateTime** 有効桁数に切り捨てられます。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 のプログラミング概念](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
