---
title: バックアップ ファイルはデータベース ファイルとは別のデバイスに配置する
description: SQL Server でポリシーベースの管理を行うためのデータベース ファイルの場所とバックアップ ファイルの場所を比較するためのポリシーを有効にする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 5b98f8163a3564ccc4aadac6c71c30eb5cf37697
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285243"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>バックアップ ファイルはデータベース ファイルとは別のデバイスに配置する
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、データベース ファイルがバックアップ ファイルとは異なるデバイス上にあるかどうかを確認します。 データベース ファイルとバックアップ ファイルが同じデバイスにある場合、デバイスに障害が発生すると、データベースとバックアップの両方が使用できなくなります。 また、データベースとバックアップ ファイルを異なるデバイスに置くと、データベースの運用でもバックアップの書き込みでも I/O パフォーマンスが最適化されます。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスの推奨事項  
 バックアップ ディスクには、データベースのデータ ディスクやログ ディスクとは別のディスクを使用することをお勧めします。 これは、データ ディスクやログ ディスクで障害が発生した場合に確実にバックアップにアクセスできるようにするために必要です。

データベース ファイルとバックアップ ファイルが同じデバイスにある場合、デバイスに障害が発生すると、データベースとバックアップの両方が使用できなくなります。 また、データベースとバックアップ ファイルを異なるデバイスに置くと、データベースの運用でもバックアップの書き込みでも I/O パフォーマンスが最適化されます。
  
## <a name="see-also"></a>関連項目 
   
  
 [バックアップ デバイス](../backup-restore/backup-devices-sql-server.md)  
  
