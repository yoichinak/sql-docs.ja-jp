---
title: LocalDB のサポート
description: LocalDB インスタンス内のデータベースに接続する方法について説明します。これは SQL Server Native Client でサポートされている SQL Server の軽量バージョンです。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fcbd82f5752075ead64c22e61d92a2f32066b259
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892282"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client における LocalDB のサポート
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降、SQLServer の簡易バージョンである LocalDB を使用できるようになります。 ここでは、LocalDB インスタンス内のデータベースに接続する方法について説明します。  
  
## <a name="remarks"></a>解説  
 LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、以下を参照してください。  
  
-   [SQL Server Express LocalDB リファレンス](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-express-localdb.md)  
  
 要約すると、LocalDB では次の操作を実行できます。  
  
-   **sqllocaldb.exe i** を使用して既定のインスタンスの名前を検出できます。  
  
-   **AttachDBFilename** 接続文字列キーワードを使用して、サーバーをアタッチするデータベース ファイルを指定できます。 **AttachDBFilename** を使用するときに、**Database** 接続文字列キーワードを使用してデータベース名を指定しなかった場合、データベースはアプリケーションの終了時に LocalDB インスタンスから削除されます。  
  
-   接続文字列では、次のように LocalDB インスタンスを指定します。  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要に応じて、sqllocaldb.exe を使用して LocalDB インスタンスを作成できます。 また、sqlcmd.exe を使用して、LocalDB インスタンスのデータベースの追加と変更を実行できます。 たとえば、**sqlcmd -S (localdb)\v11.0** のようにします。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
