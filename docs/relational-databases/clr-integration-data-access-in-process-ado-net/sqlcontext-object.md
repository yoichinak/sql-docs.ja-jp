---
title: SqlContext オブジェクト |Microsoft Docs
description: ユーザー接続の SQL Server でマネージコードを呼び出すと、呼び出し元のコンテキストへのアクセスが SqlContext オブジェクトで抽象化されます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
ms.openlocfilehash: c423b4d2b6296da5ce95e62bfc51a160beb956a5
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810730"
---
# <a name="sqlcontext-object"></a>SqlContext オブジェクト
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  プロシージャや関数の呼び出し時、CLR (共通言語ランタイム) ユーザー定義型のメソッドの呼び出し時、または任意の [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 言語で定義されたトリガーの起動時には、サーバーのマネージド コードを呼び出します。 このコードの実行はユーザー接続の一環として要求されるので、サーバーで実行しているコードから呼び出し元のコンテキストにアクセスできる必要があります。 また、特定のデータ アクセス操作には、コードが呼び出し元のコンテキストで実行されている場合にしか有効にならないものもあります。 たとえば、トリガー操作で使用される inserted 擬似テーブルや deleted 擬似テーブルにアクセスするには、コードが呼び出し元のコンテキストで実行されている必要があります。  
  
 呼び出し元のコンテキストは、 **Sqlcontext** オブジェクトで抽象化されています。 **Sqltriggercontext**のメソッドとプロパティの詳細については、SDK の「 **Microsoft. SqlServer. sqltriggercontext**クラスのリファレンスドキュメント」を参照してください。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  
  
 **Sqlcontext** は、次のコンポーネントへのアクセスを提供します。  
  
-   **SqlPipe**: **SqlPipe** オブジェクトは、結果がクライアントに流れる "パイプ" を表します。 **SqlPipe**オブジェクトの詳細については、「 [SqlPipe オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)」を参照してください。  
  
-   **Sqltriggercontext**: **sqltriggercontext** オブジェクトは、CLR トリガー内からのみ取得できます。 このオブジェクトでは、トリガーを起動した操作や、更新された列のマップについての情報を提供します。 **Sqltriggercontext**オブジェクトの詳細については、「 [sqltriggercontext オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)」を参照してください。  
  
-   **IsAvailable**: **IsAvailable** プロパティは、コンテキストの可用性を決定するために使用されます。  
  
-   **WindowsIdentity**: **WindowsIdentity** プロパティは、呼び出し元の Windows id を取得するために使用されます。  
  
## <a name="determining-context-availability"></a>コンテキスト可用性の判断  
 **Sqlcontext**クラスに対してクエリを実行し、現在実行中のコードがインプロセスで実行されているかどうかを確認します。 これを行うには、 **Sqlcontext**オブジェクトの**IsAvailable**プロパティを確認します。 **IsAvailable**プロパティは読み取り専用であり、呼び出し元**True**のコードが内で実行されていて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 他の**sqlcontext**メンバーにアクセスできる場合は True を返します。 **IsAvailable**プロパティが**False**を返した場合は、他のすべての**sqlcontext**メンバーが**InvalidOperationException**をスローします (使用されている場合)。 **IsAvailable**から**False**が返された場合、接続文字列で "context connection = true" を持つ接続オブジェクトを開こうとすると失敗します。  
  
## <a name="retrieving-windows-identity"></a>Windows ID の取得  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で実行されている CLR コードは、常に、プロセス アカウントのコンテキストで呼び出されます。 コードで、プロセス id ではなく、呼び出し元ユーザーの id を使用して特定のアクションを実行する必要がある場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sqlcontext**オブジェクトの**WindowsIdentity**プロパティを使用して権限借用トークンを取得する必要があります。 **WindowsIdentity**プロパティは、呼び出し元の Windows id を表す**WindowsIdentity**インスタンスを返し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。または、クライアントが認証を使用して認証された場合は null を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このプロパティにアクセスできるのは、 **EXTERNAL_ACCESS** または **UNSAFE** アクセス許可でマークされたアセンブリだけです。  
  
 **WindowsIdentity**オブジェクトを取得した後、呼び出し元はクライアントアカウントの権限を借用し、ユーザーに代わってアクションを実行できます。  
  
 ストアドプロシージャまたは関数の実行を開始したクライアントが Windows 認証を使用してサーバーに接続している場合、呼び出し元の id は Sqlcontext を通じてのみ使用でき**ます。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が使用されている場合、このプロパティは NULL になり、コードでは呼び出し元ユーザーの権限を借用することはできません。  
  
### <a name="example"></a>例  
 次の例では、呼び出し元であるクライアントの Windows ID を取得し、クライアントの権限を借用する方法を示します。  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>参照  
 [SqlPipe オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR トリガー](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
