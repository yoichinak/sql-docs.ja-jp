---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215144"
---
SQL Server 2019 CU5 以降、基本認証で新しいクラスターを展開すると、ゲートウェイを含むすべてのエンドポイントで `AZDATA_USERNAME` と `AZDATA_PASSWORD` が使用されます。 CU5 にアップグレードされるクラスターのエンドポイントでは、ゲートウェイ エンドポイントに接続するとき、ユーザー名として `root` が引き続き使用されます。 この変更は、Active Directory 認証による展開には適用されません。 このリリース ノートの「[ゲートウェイ エンドポイント経由でサービスにアクセスするための資格情報](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint)」を参照してください。