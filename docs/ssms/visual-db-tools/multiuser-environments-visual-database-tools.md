---
description: マルチユーザー環境 (Visual Database Tools)
title: マルチユーザー環境
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 7b31540ad30056e3f4a3b6d34c2bb57912e304a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423116"
---
# <a name="multiuser-environments-visual-database-tools"></a>マルチユーザー環境 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
マルチユーザー環境とは、複数のユーザーが同じデータベースに同時に接続し、変更を行うことができる環境です。 その結果、複数のユーザーが同時に同じデータベース オブジェクトに対する作業を行う場合があります。 したがって、マルチユーザー環境では、あるユーザーが使用しているデータベースが、自身が変更を行っている最中に他のユーザーが行った変更による影響を受ける可能性があります。  
  
マルチユーザー環境のデータベースで作業するときの重要な問題はアクセス許可です。 データベースに対してユーザーが持っているアクセス許可により、ユーザーがそのデータベースについて行うことができる作業の範囲が決まります。 たとえば、データベースのオブジェクトを変更するには、データベースに対する適切な書き込みアクセス許可が必要です。 データベースでのアクセス許可の詳細については、使用しているデータベースのドキュメントを参照してください。 詳しくは、「[アクセス許可と Visual Database Tools (Visual Database Tools)](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md)」をご覧ください。  
  
テーブルに行った変更を保存する際に、そのユーザーが最後にテーブルへの変更を保存してからデータベースが変更されていないかどうか、テーブル デザイナーによって確認が行われます。 他のユーザーが変更を行っていた場合は、データベースが変更されていることが通知されます。 これらの変更は調整する必要があります。 詳しくは、「[複数のユーザーによる変更の調整 (Visual Database Tools)](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md)」をご覧ください。  
  
マルチユーザー環境では、競合する変更を避けるために特に注意が必要なことがあります。 詳しくは、「[運用されているデータベースを変更するときの問題 (Visual Database Tools)](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md)」をご覧ください。  
  
問題を回避する方法の 1 つは、変更を行う場合に、テスト データベースなどのデータベースのコピーを使用することです。さらに変更点を元のデータベースに反映する変更スクリプトを作成し、オフラインで競合の問題を解消した後で、実行します。 詳しくは、「[開発用データベース、テスト用データベース、および実行時用データベース (Visual Database Tools)](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md)」をご覧ください。  
  
