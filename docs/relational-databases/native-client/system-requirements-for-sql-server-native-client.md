---
description: SQL Server Native Client のシステム要件
title: システム要件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27e6a98231e66a24a66233092e3e7e245a4e3d74
ms.sourcegitcommit: 5dcbe4abbe2339292961370c1d8ca3affa625f72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "99536401"
---
# <a name="system-requirements-for-sql-server-native-client"></a>SQL Server Native Client のシステム要件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ アクセス機能 (MARS など) を使用するには、次のソフトウェアがインストールされている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (クライアント)  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス (サーバー)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client には Windows インストーラー3.1 が必要です。 Windows インストーラー3.1 は、Windows オペレーティングシステムに既にインストールされてい [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 他のすべてのプラットフォームには、明示的にインストールする必要があります。 詳細については、「 [Windows インストーラー3.1 再頒布可能パッケージ (v2)](https://www.microsoft.com/download/details.aspx?id=25)」を参照してください。  
  
> [!NOTE]  
>  このソフトウェアは、必ず管理者特権でログオンしてからインストールしてください。  
  
## <a name="operating-system-requirements"></a>オペレーティング システムの要件  
 Native Client をサポートするオペレーティングシステムの一覧につい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ては、「 [SQL Server Native Client のサポートポリシー](../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md)」を参照してください。  
  
## <a name="sql-server-requirements"></a>SQL Server の要件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータにアクセスするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがインストールされている必要があります。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、MDAC、Windows Data Access Components、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のすべてのバージョンからの接続をサポートします。 古いクライアント バージョンで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する場合、クライアントで認識されないサーバーのデータ型は、クライアント バージョンと互換する型にマップされます。 詳細については、このトピックの「クライアント バージョンのデータ型の互換性」をご覧ください。  
  
## <a name="cross-language-requirements"></a>言語間の要件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の英語版は、サポートされているオペレーティング システムであれば、そのすべてのローカライズ版でもサポートされます。 ネイティブクライアントのローカライズ版は、ローカライズされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] たネイティブクライアントバージョンと同じ言語のローカライズされたオペレーティングシステムでサポートされてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ローカライズされたバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、対応する言語設定がインストールされている限り、サポートされているオペレーティングシステムの英語版でもサポートされています。  
  
 アップグレードの要件を次に示します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の英語版は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のどのローカライズ版にもアップグレードできます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のローカライズ版は、同じ言語にローカライズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client にアップグレードできます。  
  
-   Native Client のローカライズ版は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、英語版の Native client にアップグレードでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のローカライズ版は、異なる言語にローカライズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client にはアップグレードできません。  
  
## <a name="data-type-compatibility-for-client-versions"></a>クライアント バージョンのデータ型の互換性  
 以下の表に示すように、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は新しいデータ型を、下位クライアントと互換する古いデータ型にマップします。  
  
 OLE DB と ADO アプリケーションでは、Native Client で **DataTypeCompatibility** 接続文字列キーワードを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 古いデータ型を操作できます。 **DataTypeCompatibility=80** の場合、OLE DB クライアントは TDS (表形式データ ストリーム) バージョンではなく、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] TDS バージョンを使用して接続します。 つまり、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のデータ型の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ではなく、サーバーによって下位変換が実行されます。 またこの場合は、接続で使用可能な機能が、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 機能セットに制限されます。 新しいデータ型または機能を使用しようとすると、API 呼び出し時にすぐに検出されます。無効な要求はサーバーに渡されず、呼び出し元のアプリケーションにエラーが返されます。  
  
 ODBC の **DataTypeCompatibility** コントロールはありません。  
  
 IDBInfo::GetKeywords からは、接続のサーバー バージョンに対応し、**DataTypeCompatibility** の影響を受けないキーワードの一覧が常に返されます。  
  
|データ型|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components、MDAC、<br /><br /> DataTypeCompatibility=80 が設定された SQL Server Native Client OLE DB アプリケーション|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|Image|  
|varchar(max)|varchar|varchar|Text|  
|nvarchar(max)|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|Ntext|  
|CLR UDT (> 8 Kb)|udt|varbinary|Image|  
|date|date|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [SQL Server Native Client のインストール](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
