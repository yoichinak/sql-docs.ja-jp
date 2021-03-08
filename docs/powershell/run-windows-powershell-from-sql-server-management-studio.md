---
title: SQL Server Management Studio から Windows PowerShell を実行する方法
description: パスが、選択したオブジェクトの場所にあらかじめ設定されている場合に、SQL Server Management Studio のオブジェクト エクスプローラーから Windows PowerShell セッションを開始する方法について説明します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 03/14/2017
ms.openlocfilehash: 9fd9b7039680b05515d1f70102408394b5443c9c
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101839469"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から Windows PowerShell を実行する方法

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Windows PowerShell セッションは、SQL Server Management Studio (SSMS) の **オブジェクト エクスプローラー** から開始できます。 SSMS によって Windows PowerShell が起動され、**SqlServer** モジュールが読み込まれて、パス コンテキストが、**オブジェクト エクスプローラー** ツリー内の関連ノードに設定されます。

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

**オブジェクト エクスプローラー** でオブジェクトに対して PowerShell の実行を指定すると、SQL Server PowerShell スナップインの読み込みと登録が完了した Windows PowerShell セッションが SQL Server Management Studio によって開始されます。 セッションのパスは、オブジェクト エクスプローラーで右クリックしたオブジェクトの場所にあらかじめ設定されています。

たとえば、オブジェクト エクスプローラーで AdventureWorks データベース オブジェクトを右クリックして **[PowerShell の起動]** をクリックした場合、Windows PowerShell パスは次に示すように設定されます。

```powershell
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```

## <a name="run-powershell"></a>PowerShell の実行

### <a name="to-run-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から PowerShell を実行するには

1. **オブジェクト エクスプローラー** を開きます。

2. 作業対象オブジェクトのノードに移動します。

3. オブジェクトを右クリックし、 **[PowerShell の起動]** を選択します。

## <a name="permissions"></a>アクセス許可

PowerShell を SQL Server Management Studio で開いた場合は管理者特権で実行されないため、WMI の呼び出しなどの一部のアクティビティが実行されない場合があります。

## <a name="see-also"></a>参照

- [SQL Server PowerShell](sql-server-powershell.md)