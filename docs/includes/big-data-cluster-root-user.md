---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: 599b4072c5d03c8a4753c7c00bc7edc14e0f3b05
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100038949"
---
SQL Server 2019 CU5 以降、基本認証で新しいクラスターを展開すると、ゲートウェイを含むすべてのエンドポイントで `AZDATA_USERNAME` と `AZDATA_PASSWORD` が使用されます。 CU5 にアップグレードされるクラスターのエンドポイントでは、ゲートウェイ エンドポイントに接続するとき、ユーザー名として `root` が引き続き使用されます。 この変更は、Active Directory 認証による展開には適用されません。 このリリース ノートの「[ゲートウェイ エンドポイント経由でサービスにアクセスするための資格情報](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint)」を参照してください。