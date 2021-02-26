---
title: 構成管理に対応したビッグ データ クラスターへのアップグレード
titleSuffix: SQL Server big data clusters
description: 構成管理に対応したビッグ データ クラスターへのアップグレード
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/11/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0a9f6addcf73e0c50d67f75f19fedd51b2f3dbc9
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100344011"
---
# <a name="upgrading-to-a-configuration-management-enabled-cluster-cu8-or-lower-to-cu9"></a>構成管理に対応したクラスターへのアップグレード (CU8 以前から CU9 以降へ)

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]
CU9 以降、ビッグ データ クラスターには構成管理機能が含まれています。管理者はこの機能を使用して、ビッグ データ クラスター配置後のさまざまな部分を変更または調整し、BDC で実行している構成に関する詳細な分析情報を得ることができます。 CU9 より前には、通常、ビッグ データ クラスターの構成は配置時にしか変更できず、カスタム `mssql-custom.conf` ファイルを使用して一部の SQL 構成を構成することが回避策になっていました。 現在、この回避策は解決済みであり、それらの設定は構成管理機能を使用して構成できます。

## <a name="migrating-sql-configurations-in-mssql-customconf-to-the-configuration-management-system"></a>mssql-custom.conf 内の SQL 構成を構成管理システムに移行する
SQL Server マスター インスタンスのカスタム `mssql-custom.conf` を作成した場合は、ファイルではなく構成システムを使用して設定を管理するために、次に示す 1 回限りの手順に従ってください。 これらの手順を行わないと、それらの SQL 構成は構成管理機能で管理されず、構成管理機能を使用してそれらの設定に加えた変更は、`mssql-custom.conf` の設定によってオーバーライドされます。

手順:
1. ビッグ データ クラスターを CU9 にアップグレードします
> [!NOTE]
> `mssql-custom.conf` で定義した設定は、変更または削除されません。 構成フレームワークによる適用および管理が行われないだけです。

2. `mssql-custom.conf` で以前に定義したすべての設定を、新しい構成機能を使用して設定し、適用します。 設定を変更するためのステップ バイ ステップ ガイドについては、「[SQL Server ビッグ データ クラスター配置後の構成の概要](configure-bdc-postdeployment.md)」を参照してください。 各スコープで使用可能な設定の一覧については、「[SQL Server ビッグ データ クラスターの構成プロパティ](reference-config-bdc-overview.md)」を参照してください。 customerFeedback のような一部の設定はスコープが変更されている可能性がありますが、引き続き使用可能です。
3. 各マスター ポッドの `mssql-server` コンテナー内にある `mssql-custom.conf` ファイルの名前を `deprecated-mssql-custom.conf` に変更します。 マスターが 1 つ (`master-0`) しかない場合。 構成に対応していないクラスター (CU8 以前) へのダウングレードまたはロールバックが必要な場合は、このファイルを再利用して、これらのカスタム SQL 構成を適用することができます。

## <a name="downgrading-from-a-configuration-management-enabled-cluster-to-a-non-configuration-management-enabled-cluster-cu9-to-cu8-or-lower"></a>構成管理に対応したクラスターから構成管理に対応していないクラスターに (CU9 以降から CU8 以前に) ダウングレードする
構成管理に対応したクラスター (CU9 以降) から構成管理に対応していないクラスター (CU8 以前) にダウングレードすると、ビッグ データ クラスター配置後の調整の機能が削除されます。 また、オプションの `mssql-custom.conf` ファイルを使用して SQL 構成を設定する必要があります。 CU9 以降にアップグレードしたときにファイルの名前を `deprecated-mssql-custom.conf` に変更した場合は、名前を `mssql-custom.conf` に戻します。 ファイルを削除した場合、または以前に作成したことがなく、これらの特別な SQL 構成を定義することが必要になった場合は、「[SQL Server マスター インスタンスの構成プロパティ - CU9 より前のリリース](reference-config-master-instance.md)」に記載されている手順に従って作成します。 構成管理操作によって定義および変更したすべての設定は、以前の構成またはシステムの既定値に戻されます。 

クラスターをダウングレードすると、設定は既定値または配置の bdc.js で指定した値に戻ります。 ダウングレード後に他の手順は必要ありません。