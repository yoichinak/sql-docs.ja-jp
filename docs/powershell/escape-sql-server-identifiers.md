---
title: SQL Server 識別子のエスケープ
description: SQL Server の区切られた識別子に使用できる文字には、Windows PowerShell パスでサポートされないものがあります。 これらの一部をバック ティック文字でエスケープする方法について学習します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 105acf1e3e67d558ccbb0ae450afba9468de3a5f
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101838032"
---
# <a name="escape-sql-server-identifiers"></a>SQL Server 識別子のエスケープ

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の区切られた識別子には使用でき、Windows PowerShell パス名には使用できない文字をエスケープするためによく使用されるのが、バック ティック エスケープ文字 (`) です。 ただし、エスケープできない文字もあります。 たとえば、Windows PowerShell ではコロン文字 (:) をエスケープできません。 この文字を含んだ識別子は、エンコードする必要があります。 エンコードは、すべての文字に有効であるため、エスケープよりも確実です。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

通常、バック ティック文字 (`) のキーは、キーボード左上の Esc キーの下にあります (英語キーボードの場合)。  

## <a name="examples"></a>例

次に示すのは、# 文字をエスケープする例です。  

```powershell
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```

次に示すのは、コンピューター名として (local) を指定する際に、かっこをエスケープする例です。  

```powershell
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```

## <a name="see-also"></a>参照

- [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)
- [SQL Server PowerShell プロバイダー](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)