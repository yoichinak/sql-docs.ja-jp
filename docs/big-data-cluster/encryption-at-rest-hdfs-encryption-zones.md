---
title: SQL Server ビッグ データ クラスター HDFS 暗号化ゾーンの使用ガイド
titleSuffix: SQL Server big data clusters
description: この記事では、BDC の SQL Server HDFS 暗号化ゾーン機能の使用方法について説明します。
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4c56d065de396a282c97c0723f118e5911617544
ms.sourcegitcommit: e8c0c04eb7009a50cbd3e649c9e1b4365e8994eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2021
ms.locfileid: "100489296"
---
# <a name="sql-server-big-data-clusters-hdfs-encryption-zones-usage-guide"></a>SQL Server ビッグ データ クラスター HDFS 暗号化ゾーンの使用ガイド

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このガイドでは、SQL Server ビッグ データ クラスターの保存時の暗号化機能を使用し、暗号化ゾーンを使用して HDFS フォルダーを暗号化する方法について説明します。 HDFS のキー管理タスクについても説明します。

使用できる状態になっている、マウントされた既定の暗号化ゾーンが __```/securelake```__ に存在することに注意してください。 これは、__securelakekey__ という名前のシステム生成の 256 ビット キーを使用して作成されました。 このキーは、追加の暗号化ゾーンを作成するために使用できます。

## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- [Active Directory](active-directory-prerequisites.md) 統合を使用する [SQL Server ビッグ データ クラスター CU8 以降](release-notes-big-data-cluster.md)。
- 管理特権を持つユーザー。
- AD モードで構成され、クラスターにログインしている [!INCLUDE[azdata](../includes/azure-data-cli-azdata.md)]。

## <a name="create-an-encryption-zone-using-the-provided-system-managed-key"></a>指定されたシステム マネージド キーを使用して暗号化ゾーンを作成する

1. HDFS フォルダーを作成します

   ```console
   azdata bdc hdfs mkdir -p /user/zone/folder
   ```

1. encryption zone create コマンドを発行して、__securelakekey__ キーを使用してフォルダーを暗号化します。

   ```console
   azdata bdc hdfs encryption-zone create --path /user/zone/folder --keyname securelakekey
   ```

## <a name="create-a-custom-new-key-and-encryption-zone"></a>カスタムの新しいキーと暗号化ゾーンを作成する

1. 次のパターンを使用して、256 ビットのキーを作成します。

   ```console
   azdata bdc hdfs key create -n mydatalakekey
   ```

1. ユーザー キーを使用して、新しい HDFS パスを作成し、暗号化します。

   ```console
   azdata bdc hdfs encryption-zone create --path /user/mydatalake --keyname mydatalakekey
   ```

## <a name="hdfs-key-rotation-and-encryption-zone-re-encryption"></a>HDFS キーのローテーションと暗号化ゾーンの再暗号化

1. 新しいキー マテリアルを使用して __securelakekey__ の新しいバージョンが作成されます。

   ```console
   azdata hdfs bdc key roll -n securelakekey
   ```

1. 上記のキーに関連付けられている暗号化ゾーンを再暗号化します。

   ```console
   azdata bdc hdfs encryption-zone reencrypt --path /securelake --action start
   ```

## <a name="hdfs-key-and-encryption-zone-monitoring"></a>HDFS キーと暗号化ゾーンの監視

1. 暗号化ゾーンの再暗号化の状態を監視するには 

   ```console
   azdata bdc hdfs encryption-zone status
   ```

1. 暗号化ゾーン内のファイルに関する暗号化情報を取得するには

   ```console
   azdata bdc hdfs encryption-zone get-file-encryption-info --path /securelake/data.csv
   ```

1. すべての暗号化ゾーンを一覧表示する

   ```console
   azdata bdc hdfs encryption-zone list
   ```

1. HDFS で使用可能なすべてのキーを一覧表示するには

   ```console
   azdata bdc hdfs key list
   ```

1. HDFS 暗号化用のカスタム キーを作成するために、 指定できるサイズは 128、192、256 です。 既定値は 256 です

   ```console
   azdata hdfs key create --name key1 --size 256
   ```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターで azdata を使用する方法については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] とは](big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する
