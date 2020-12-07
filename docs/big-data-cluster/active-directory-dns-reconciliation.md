---
title: ビッグ データ クラスターの展開での Active Directory と Kubernetes の DNS の調整
description: Active Directory モードの SQL Server ビッグ データ クラスターに対する DNS の調整を構成する
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63a5c53e64ece7650e65414fd24ddd82d6da5324
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892462"
---
# <a name="active-directory-and-kubernetes-dns-reconciliation-in-big-data-clusters-deployments"></a>ビッグ データ クラスターの展開での Active Directory と Kubernetes の DNS の調整

この記事では、ビッグ データ クラスター (BDC) を展開するときに Active Directory の統合に対応するための課題と解決策について説明します。

## <a name="overview"></a>概要

ビッグ データ クラスターが Active Directory の統合を使用して展開されていない場合、内部 DNS の解決には [Kubernetes CoreDNS](https://kubernetes.io/docs/tasks/administer-cluster/coredns/) サービスを利用します。 Kubernetes では、`<namespace>.svc.cluster.local` などの内部ドメインが使用されます。 このドメイン内の名前を使用して、DNS サーバーに A (前方参照) レコードと PTR (逆引き参照) レコードが作成されます。

しかし、Active Directory モードが有効になっていると、新しいドメインでは独自の DNS サーバーのセットが関係します。 このため、内部的な名前解決の間に、DNS サーバーのセットによる前方参照と逆引き参照のための移動で混乱が発生する可能性があります。

## <a name="challenges"></a>課題

* 新しい Kubernetes ポッドが展開されるとき、DNS サーバーの両方のセットに DNS エントリが追加される必要があります。 しかし、CoreDNS へのエントリの記録は Kubernetes によって行われ、Active Directory ドメイン コントローラーの DNS サーバーへの必要なエントリの追加は BDC 展開ワークフローによって行われます。 同様に、BDC クラスターが削除されるときは、ワークフローでこれらのエントリが確実に削除されるようにする必要があります。
* Active Directory の DNS サーバーは、Kubernetes クラスターの外部にあります。 しかし、BDC には Kubernetes 内に独自の IP 空間があり、この IP 空間はクラスター境界の外部からは見えないため、外部に配置された DNS サーバーにこの IP 空間のレコードを作成することはできません。
* Kubernetes クラスター内でフェールオーバー イベントが発生したら、AD DNS サーバー内のレコードも更新する必要があります。
* ポッド名に加えて、Kubernetes サービスの名前も、AD のドメイン名参照によってアドレス指定できる必要があります。 これにより、1 つのサービス名をポッドの複数の IP アドレスにマップできるため、Active Directory DNS で新しい課題が発生します。
* 組織の Active Directory DNS サーバーでのレコード更新の伝達とレプリケーションにおける遅延が大きくなり、BDC 管理ワークフローの制御が及ばなくなる可能性があります。 これにより、展開とフェールオーバーの直後に BDC の機能が影響を受ける可能性があります。 反対に、Kubernetes CoreDNS は、その局所性により、高速で効率的です。

## <a name="solution"></a>解決策

前述の課題に対処するため、BDC で実装されるソリューションには、BDC 名前空間内で管理される新しい内部 CoreDNS サービスが含まれます。 これは、BDC 名前空間のポッドが名前解決のために接続する唯一の DNS サービスです。 複数のドメインの複雑さは、新しい CoreDNS サービスの背後に隠されます。

たとえば、次の図のポッドでは、BDC CoreDNS サーバーを使用して名前が解決されています。 ポッドと、Kubernetes CoreDNS サーバーまたは AD DNS サーバーの間で、直接やり取りされることはありません。 

:::image type="content" source="media/active-directory-dns-reconciliation/bdc-ad-dns-reconciliation.png" alt-text="ポッドは、独自の名前空間内の CoreDNS サーバーに接続する":::

以下では、この設計の BDC での機能を明確にする実装の詳細について説明します。

### <a name="centralized-management-of-multiple-domains"></a>複数のドメインの集中管理

名前参照で発生する処理の複雑さは、一元化されて内部 DNS サービスの背後に隠されたままになります。 これにより、複数のドメインを管理する負担が個々のポッドにかかることがなくなり、設計が簡素化されます。

### <a name="no-records-for-internal-pods-in-external-dns-servers"></a>外部 DNS サーバーに内部ポッドに関するレコードがない

この設計原理の結果として、Kubernetes の IP 空間内にあるポッドに関する A レコードと PTR レコードを、BDC によって外部 DNS サーバーに作成して管理する必要はありません。

### <a name="no-duplication-of-records"></a>レコードの重複がない

内部 DNS レコードは複数の場所にあります。 これらのレコードの唯一のストレージは Kubernetes CoreDNS です。 BDC の内部 CoreDNS によって、DNS クエリの計算の書き換えと Kubernetes CoreDNS への転送が行われます。

### <a name="computational-rewriting"></a>計算の書き換え

BDC にはレコードが格納されないため、BDC では、AD ドメインの名前が使用されている受信前方参照クエリを Kubernetes ドメインの名前に変換し、このクエリを Kubernetes CoreDNS に転送する必要があります。
たとえば、`compute-0-0.contoso.local` に対する受信クエリは `compute-0-0.compute-0-svc.contoso.svc.cluster.local` に書き換えられ、この要求が Kubernetes CoreDNS に転送されます。
逆引き参照の場合は、Kubernetes CoreDNS へのときと同じようにクエリは内部 IP を使用して転送され、そこからの応答はクライアントに応答する前に AD ドメイン名に書き換えられます。

### <a name="simplicity-in-pod-configurations"></a>ポッドの構成の単純さ

すべての BDC ポッドの /etc/resolv.conf では内部 BDC CoreDNS だけが参照されるため、ポッドからのネットワーク ビューが簡略化されます。 代わりに、複雑さは内部 CoreDNS 内に隠されます。

### <a name="static-and-reliable-ip-address-for-dns-service"></a>DNS サービスに対する静的で信頼性の高い IP アドレス

BDC によって展開される CoreDNS サービスにより、すべてのポッドからアクセスできる静的内部 IP が登録されます。 これにより、/etc/resolv.conf 内の値を更新する必要がなくなります。

### <a name="service-load-balance-management-is-retained-by-kubernetes"></a>サービスの負荷分散の管理は Kubernetes によって維持される

個々のポッドではなくサービスに対して参照が行われても、それらは Kubernetes CoreDNS に送られるため、BDC に AD ドメイン固有の負荷分散を実装する必要はありません。

たとえば、`compute-0-svc.contoso.local` に対する前方参照要求は、` compute-0-svc.contoso.svc.cluster`.local に書き換えられます。 この要求は Kubernetes CoreDNS に転送され、そこで負荷分散が行われます。 応答は、複数のコンピューティング プール インスタンス (ポッド レプリカ) の 1 つに対する IP アドレスになります。

### <a name="scalability"></a>スケーラビリティ

BDC にはレコードが格納されないため、複数のレプリカの間で状態の保持とレコードのレプリケーションを行うことなく、内部 BDC CoreDNS をスケーリングできます。 DNS レコードが BDC 内に格納される場合は、すべてのポッド間での状態のレプリケートも、BDC によって処理される必要があります。

### <a name="externally-visible-service-entries-stay-in-ad-dns"></a>外部から参照可能なサービス エントリが AD DNS に維持される

Kubernetes クラスターの外部にあるクライアントからアクセスできる必要があるサービス エンドポイントの場合、BDC が展開されるときに DNS エントリが AD DNS サーバーに作成されます。 ユーザーは、展開構成プロファイルを使用して、登録する DNS 名を入力します。

### <a name="self-deprovisioning"></a>セルフプロビジョニング解除

BDC を削除した後は、クラスターをプロビジョニング解除するときに、それ以上の動的な DNS エントリ削除作業はありません。 リモート Active Directory DNS でクリーンアップが必要なエントリは外部サービスに関するものだけであり、それらの数は静的です。 内部 DNS エントリは、クラスターと共に自動的に削除されます。

## <a name="next-steps"></a>次のステップ

- [Active Directory モードで SQL Server ビッグ データ クラスターを展開する](active-directory-deploy.md)
- [Active Directory モードでビッグ データ クラスター アクセスを管理する](active-directory-objects.md)
- [同じ Active Directory ドメインに複数の SQL Server ビッグ データ クラスターをデプロイする](active-directory-deployment-background.md)
