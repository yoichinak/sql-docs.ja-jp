---
description: サービス プロバイダーとコンポーネント
title: サービスプロバイダーとコンポーネント |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: rothja
ms.author: jroth
ms.openlocfilehash: 11e105becc0d62e315b4d44de9d26c093bb27326
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037022"
---
# <a name="service-providers-and-components"></a>サービス プロバイダーとコンポーネント
サービスプロバイダーは、データストアによってネイティブでサポートされていない拡張インターフェイスを実装することによって、データプロバイダーの機能を拡張するコンポーネントです。  
  
 ユニバーサルデータアクセスは、個々の特殊なコンポーネントがデータベース機能の個別セットを実装できるようにする *コンポーネントアーキテクチャ* を提供します。また、サポートされていないストアの上に "サービス" を提供します。 したがって、各データストアに対して、拡張機能の独自の実装を提供したり、内部的にデータベース機能を実装するように汎用アプリケーションを強制するのではなく、サービスコンポーネントは、任意のデータストアにアクセスするときにアプリケーションが使用できる共通の実装を提供します。 一部の機能はデータストアによってネイティブに実装され、一部の機能は汎用コンポーネントによってアプリケーションに対して透過的に行われます。  
  
 たとえば、cursor [service for OLE DB](/previous-versions/windows/desktop/ms714397(v=vs.85))などのカーソルエンジンは、順次的な順方向専用データストアのデータを使用して、スクロール可能なデータを生成するサービスコンポーネントです。 ADO によって一般的に使用されるその他のサービスプロバイダーには、 [microsoft OLE DB 永続化プロバイダー (Ado サービスプロバイダー)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 、OLE DB (データをファイルに保存するため)、Microsoft [データ整形サービス](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (階層的な **レコードセット** 用)、 [Microsoft OLE DB リモート処理プロバイダー (ado サービスプロバイダー)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (リモートコンピューターでデータプロバイダーを呼び出す場合) などがあります。  
  
 サービスプロバイダーとデータプロバイダーの詳細については、「 [付録 a: providers](../../../ado/guide/appendixes/appendix-a-providers.md)」を参照してください。