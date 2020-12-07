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
ms.openlocfilehash: 0f0c89d8a7f83bebfa77fb02a282fc21cb6f2dd0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724943"
---
# <a name="service-providers-and-components"></a>サービス プロバイダーとコンポーネント
サービスプロバイダーは、データストアによってネイティブでサポートされていない拡張インターフェイスを実装することによって、データプロバイダーの機能を拡張するコンポーネントです。  
  
 ユニバーサルデータアクセスは、個々の特殊なコンポーネントがデータベース機能の個別セットを実装できるようにする *コンポーネントアーキテクチャ* を提供します。また、サポートされていないストアの上に "サービス" を提供します。 したがって、各データストアに対して、拡張機能の独自の実装を提供したり、内部的にデータベース機能を実装するように汎用アプリケーションを強制するのではなく、サービスコンポーネントは、任意のデータストアにアクセスするときにアプリケーションが使用できる共通の実装を提供します。 一部の機能はデータストアによってネイティブに実装され、一部の機能は汎用コンポーネントによってアプリケーションに対して透過的に行われます。  
  
 たとえば、cursor [service for OLE DB](/previous-versions/windows/desktop/ms714397(v=vs.85))などのカーソルエンジンは、順次的な順方向専用データストアのデータを使用して、スクロール可能なデータを生成するサービスコンポーネントです。 ADO によって一般的に使用されるその他のサービスプロバイダーには、 [microsoft OLE DB 永続化プロバイダー (Ado サービスプロバイダー)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 、OLE DB (データをファイルに保存するため)、Microsoft [データ整形サービス](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (階層的な **レコードセット**用)、 [Microsoft OLE DB リモート処理プロバイダー (ado サービスプロバイダー)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (リモートコンピューターでデータプロバイダーを呼び出す場合) などがあります。  
  
 サービスプロバイダーとデータプロバイダーの詳細については、「 [付録 a: providers](../../../ado/guide/appendixes/appendix-a-providers.md)」を参照してください。