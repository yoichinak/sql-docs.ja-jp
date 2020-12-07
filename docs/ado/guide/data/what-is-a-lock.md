---
description: ロックとは
title: ロックとは | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: rothja
ms.author: jroth
ms.openlocfilehash: d64d6b417f6430cb834c48b8caf93e041a2084e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978873"
---
# <a name="what-is-a-lock"></a>ロックとは
ロックは、DBMS がマルチユーザー環境の行へのアクセスを制限するプロセスです。 行または列が排他的にロックされている場合、ロックが解除されるまで、他のユーザーはロックされたデータにアクセスできません。 これにより、2人のユーザーが行の同じ列を同時に更新することができなくなります。  
  
 ロックはリソースの観点から非常に高価であり、データの整合性を維持するために必要な場合にのみ使用してください。 1秒ごとに数百または数千のユーザーが1つのレコードにアクセスしようとするデータベース (インターネットに接続されているデータベースなど) では、不要なロックによってアプリケーションのパフォーマンスが低下する可能性があります。  
  
 適切なロックオプションを選択することで、データソースと ADO カーソルライブラリが同時実行を管理する方法を制御できます。  
  
 **レコードセット**を開く前に、 **LockType**プロパティを設定して、プロバイダーが使用するロックの種類を指定します。 開いている **レコードセット** オブジェクトで使用中のロックの種類を返すには、プロパティを読み取ります。  
  
 プロバイダーは、すべてのロックの種類をサポートしていない可能性があります。 プロバイダーが要求された **LockType** 設定をサポートできない場合は、別の種類のロックに置き換えられます。 **レコードセット**オブジェクトで使用できる実際のロック機能を確認するには、 **Adupdate**と**adupdate**の[サポート](../../../ado/reference/ado-api/supports-method.md)メソッドを使用します。  
  
 [カーソル位置](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティが adUseClient に設定されている場合、 **adlockpessimistic**設定はサポートされません **。** サポートされていない値が設定されている場合、エラーは発生しません。サポートされている最も近い **LockType** が代わりに使用されます。  
  
 **LockType**プロパティは、**レコードセット**が閉じられている場合は読み取り/書き込みが可能で、開いている場合は読み取り専用です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ロックの種類](../../../ado/guide/data/types-of-locks.md)
