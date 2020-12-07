---
description: トリガーの作成、変更、および削除
title: トリガーの作成、変更、および削除
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f21a3d053513beaa131d4a7e781ee548f460a940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420206"
---
# <a name="creating-altering-and-removing-triggers"></a>トリガーの作成、変更、および削除
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]
  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Trigger> オブジェクトを使用してトリガーが表現されます。 トリガーが [!INCLUDE[tsql](../../../includes/tsql-md.md)] 起動されたときに実行されるコードは、 <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> トリガーオブジェクトのプロパティによって設定されます。 トリガーの型は、<xref:Microsoft.SqlServer.Management.Smo.Trigger> プロパティなど、<xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A> オブジェクトのその他のプロパティを使用することで設定します。 これは、親テーブルのレコードの **更新** によってトリガーが起動されるかどうかを指定するブール型プロパティです。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Trigger> オブジェクトは、従来のデータ操作言語 (DML) トリガーを表します。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のバージョンでは、データ定義言語 (DDL) トリガーもサポートされます。 DDL トリガーは、<xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> オブジェクトで表現します。  
  
## <a name="example"></a>例  
提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio .net で Visual C&#35; SMO プロジェクトを作成する](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Visual Basic でのトリガーの作成、変更、および削除  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースにある `Sales` という名前の既存のテーブル上に、更新トリガーを作成および挿入する方法を示します。 トリガーによって、テーブルの更新時、または新規レコードの挿入時に通知メッセージが送信されます。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Visual C# でのトリガーの作成、変更、および削除  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースにある `Sales` という名前の既存のテーブル上に、更新トリガーを作成および挿入する方法を示します。 トリガーによって、テーブルの更新時、または新規レコードの挿入時に通知メッセージが送信されます。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>PowerShell でのトリガーの作成、変更、および削除  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースにある `Sales` という名前の既存のテーブル上に、更新トリガーを作成および挿入する方法を示します。 トリガーによって、テーブルの更新時、または新規レコードの挿入時に通知メッセージが送信されます。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
