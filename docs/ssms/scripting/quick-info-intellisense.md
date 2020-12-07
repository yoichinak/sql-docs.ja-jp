---
title: クイック ヒント (IntelliSense)
description: IntelliSense のクイック ヒント オプションを使用して、コード内の識別子に関する完全な宣言を表示する方法について説明します。 SQL Server Management Studio では、データベース エンジン エディターと XML クエリ エディターでこのオプションを使用できます。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Quick Info option [IntelliSense]
- declarations [IntelliSense]
- IntelliSense [SQL Server], Quick Info
- identifier declarations [IntelliSense]
ms.assetid: 3c8b59f4-1922-4bde-844f-5f2306514d96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a0f2d426c940950b114687f39d7a94bedbb75cf
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036432"
---
# <a name="quick-info-intellisense"></a>クイック ヒント (IntelliSense)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense による **クイック ヒント** には、コード内の識別子に関する完全な宣言が表示されます。 識別子の上にマウスのポインターを置くと、黄色のポップアップ ウィンドウにその宣言が表示されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、データベース エンジン クエリ エディターおよび XML クエリ エディターで **クイック ヒント** を利用できます。  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL クイック ヒント  
 **クイック ヒント** には、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターに 2 種類の情報が表示されます。 デバッグ モードでない場合、 **クイック ヒント** には式の宣言が表示されます。 デバッグ モードの場合は、式の名前とその現在の値が **クイック ヒント** に表示されます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターでは、 **クイック ヒント** は、IntelliSense によってサポートされる [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文の部品でのみ利用できます。 たとえば、IntelliSense によってサポートされないデータ型を持つオブジェクトの識別子上にマウス ポインターを移動すると、そのデータ型はサポートされていない旨のメッセージが **クイック ヒント** のポップアップ ウィンドウに表示されます。  
  
## <a name="see-also"></a>参照  
 [IntelliSense でサポートされている Transact-SQL 構文](./transact-sql-syntax-supported-by-intellisense.md)  
  
