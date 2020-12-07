---
title: 接続の権限借用と資格情報 |Microsoft Docs
description: SQL Server CLR 統合では、WindowsIdentity プロパティを使用して、Windows 認証で呼び出し元の権限を借用することができます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
author: rothja
ms.author: jroth
ms.openlocfilehash: a6487b61d9c21ee86acad28413fb8a0439731b33
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810841"
---
# <a name="impersonation-and-credentials-for-connections"></a>接続の権限借用と資格情報
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR (共通言語ランタイム) 統合では、複雑な Windows 認証を使用する方が、SQL Server 認証を使用するよりもセキュリティが向上します。 Windows 認証を使用する場合には、次の点を考慮してください。  
  
 Windows に接続する SQL Server プロセスは、SQL Server Windows サービス アカウントのセキュリティ コンテキストを既定で取得します。 ただし、CLR 関数をプロキシ ID にマッピングすることにより、その発信接続に対し、Windows サービス アカウントとは異なるセキュリティ コンテキストを設定することができます。  
  
 場合によっては、サービスアカウントとして実行するのではなく、 **WindowsIdentity** プロパティを使用して呼び出し元の権限を借用することができます。 **WindowsIdentity**インスタンスは、呼び出し元のコードを呼び出したクライアントの id を表します。クライアントが Windows 認証を使用した場合にのみ使用できます。 **WindowsIdentity**インスタンスを取得した後、 **Impersonate**を呼び出してスレッドのセキュリティトークンを変更し、クライアントに代わって ADO.NET connections を開くことができます。  
  
 WindowsIdentity を呼び出すと、ローカルデータにアクセスできなくなり、システムデータにアクセスできなくなります。 データに再度アクセスするには、WindowsImpersonationContext を呼び出す必要があります。  
  
 次の例は、 **WindowsIdentity** プロパティを使用して呼び出し元の権限を借用する方法を示しています。  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  偽装における動作の変更点の詳細については、「 [SQL Server 2016 のデータベースエンジン機能における重大な変更](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」を参照してください。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ID インスタンスを取得した場合、既定では、そのインスタンスを別のコンピューターに反映できません。既定では、Windows セキュリティ インフラストラクチャによりこの操作が制限されます。 ただし、"委任" というメカニズムを使用すると、信頼関係のある複数のコンピューターに Windows ID を反映できるようになります。 委任の詳細については、TechNet の記事「[Kerberos プロトコル遷移と制約付き委任](/previous-versions/windows/it-pro/windows-server-2003/cc739587(v=ws.10))」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SqlContext オブジェクト](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
