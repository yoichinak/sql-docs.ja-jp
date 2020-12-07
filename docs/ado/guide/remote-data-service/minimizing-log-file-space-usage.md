---
description: ログ ファイルの使用領域の最小化
title: ログファイルの使用領域を最小限に抑える |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: rothja
ms.author: jroth
ms.openlocfilehash: 26d8a458b9bc1b477dd74ade09ad742c15ac73e8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721433"
---
# <a name="minimizing-log-file-space-usage"></a>ログ ファイルの使用領域の最小化
SQL Server データベースに大量のアクティビティがある場合は、ログファイルがすぐにいっぱいになる (サーバーが停止する) ことがあります。 ログファイルを **チェックポイントで切り捨てる** ように設定すると、データベースのログファイルの有効期間を大幅に延長できます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 でチェックポイントの切り捨てを有効にするには  
  
1.  Microsoft SQL Server Enterprise Manager を起動し、サーバーのツリーを開き、[データベースデバイス] ツリーを開きます。  
  
2.  この機能を有効にするデータベースの名前をダブルクリックします。  
  
3.  [ **データベース** ] タブで、[ **切り捨て**] を選択します。  
  
4.  [ **オプション** ] タブで、[ **チェックポイント時にログを切り捨てる**] を選択し、[ **OK**] をクリックします。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 でチェックポイントの切り捨てを有効にするには  
  
1.  Microsoft SQL Server Enterprise Manager を起動し、サーバーのツリーを開き、[データベース] ツリーを開きます。  
  
2.  この機能を有効にするデータベースの名前を右クリックし、[ **プロパティ**] を選択します。  
  
3.  [ **オプション** ] タブで、[ **チェックポイント時にログを切り捨てる**] を選択し、[ **OK**] をクリックします。  
  
 **チェックポイントの切り捨て**機能の詳細については、Microsoft SQL Server のドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [RDS の基礎](./rds-fundamentals.md)