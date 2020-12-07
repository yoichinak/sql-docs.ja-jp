---
description: 十分な TempDB 領域の確保
title: 十分な TempDB 領域を確保する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: rothja
ms.author: jroth
ms.openlocfilehash: 2842d51c09585a9b954761ac31484e4cf717a9b4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724723"
---
# <a name="ensuring-sufficient-tempdb-space"></a>十分な TempDB 領域の確保
Microsoft SQL Server 6.5 の処理領域を必要とする [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトの処理中にエラーが発生した場合は、TempDB のサイズを大きくすることが必要になることがあります。 (クエリによっては、一時的な処理領域が必要になる場合があります。たとえば、ORDER BY 句を使用するクエリには、いくつかの一時領域を必要とする **レコードセット**の並べ替えが必要です)。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
> [!IMPORTANT]
>  展開後にデバイスを圧縮するのは簡単ではないため、操作を実行する前にこの手順をお読みください。  
  
> [!NOTE]
>  既定では、inMicrosoft SQL Server 7.0 以降では、TempDB は必要に応じて自動的に拡張されるように設定されます。 このため、この手順が必要になるのは、7.0 より前のバージョンを実行しているサーバーだけです。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>SQL Server 6.5 の TempDB 領域を増やすには  
  
1.  Microsoft SQL Server Enterprise Manager を起動し、サーバーのツリーを開き、[データベースデバイス] ツリーを開きます。  
  
2.  展開する (物理) デバイス ([Master] など) を選択し、デバイスをダブルクリックして [ **データベースデバイスの編集** ] ダイアログボックスを開きます。  
  
     このダイアログボックスには、現在のデータベースで使用されている領域が表示されます。  
  
3.  [ **サイズ** ] ボックスで、デバイスを目的の量に増やします (たとえば、ハードディスク領域の 50 mb)。  
  
4.  [ **今すぐ変更** ] をクリックして、(論理) TempDB を拡張できる領域を増やします。  
  
5.  サーバーで [データベース] ツリーを開き、[ **TempDB** ] をダブルクリックして [ **データベースの編集** ] ダイアログボックスを開きます。 [ **データベース** ] タブには、現在 TempDB に割り当てられている領域の**サイズ (データサイズ**) が表示されます。 既定値は 2 MB です。  
  
6.  [ **サイズ** ] グループの [ **展開**] をクリックします。 グラフには、各物理デバイスで使用可能な領域と割り当てられた領域が表示されます。 茶色のバーは、使用可能な領域を表します。  
  
7.  [Master] などの **ログデバイス**を選択すると、[ **サイズ (MB)** ] ボックスに使用可能なサイズが表示されます。  
  
8.  [ **今すぐ展開** ] をクリックして、その領域を TempDB データベースに割り当てます。  
  
     [ **データベースの編集** ] ダイアログボックスに、TempDB に割り当てられた新しいサイズが表示されます。  
  
 このトピックの詳細については、Microsoft SQL Server Enterprise Manager のヘルプファイルで [データベースの展開] ダイアログボックスを検索してください。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)