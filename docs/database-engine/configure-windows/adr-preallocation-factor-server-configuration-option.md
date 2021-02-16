---
title: ADR 事前割り当て係数の構成オプション | Microsoft Docs
description: ADR 事前割り当て係数の SQL Server インスタンス構成設定について説明します。
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR Preallocation Factor
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9469b5de278c01b7b256ee348380ebd1ae19cde4
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347461"
---
# <a name="adr-preallocation-factor-configuration-option"></a>ADR 事前割り当て係数の構成オプション

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019 で導入されました。

この構成設定は、[高速データベース回復](../../relational-databases/accelerated-database-recovery-concepts.md)に必要です。

高速データベース復旧 (ADR) は、回復のためにデータのバージョンを保持します。 これらのバージョンは、さまざまなデータ操作言語 (DML) 操作の一部として生成されます。 バージョンは、永続バージョン ストア (PVS) と呼ばれる内部テーブルに格納されます。 

## <a name="remarks"></a>解説  

フォアグラウンド ユーザーの DML 操作の一部として PVS テーブルにページが割り当てられていると、パフォーマンスが低下することがあります。 これに対処するために、ページを事前に割り当て、DML トランザクションですぐに使用できるようにするバックグラウンド スレッドがあります。 バックグラウンド スレッドが十分なページを事前に割り当てており、フォアグラウンド PVS 割り当ての割合が 0 に近い場合、パフォーマンスが最高になります。 割合が高く、パフォーマンスに影響を与えている場合、エラー ログにタグ `PreallocatePVS` が付いたエントリが含まれます。

バックグラウンド スレッドが事前に割り当てるページ数は、さまざまなワークロード ヒューリスティックに基づいていますが、ページは主に 512 ページのチャンク単位で割り当てられます。 ADR 事前割り当て係数は、チャンクの倍数です。 既定の係数は 4 です。 これは、必要な場合、1 回に 2048 ページを事前割り当てすることを意味します。 

バックグラウンド スレッドはワークロード パターンを考慮しますが、パフォーマンスの向上に必要な場合は、係数を増やすことができます。

> [!CAUTION]
> PVS の事前割り当てが過剰に増えると、システム内の他の割り当てと競合し、実際には全体的なパフォーマンスが低下する可能性があります。
>
> この設定を変更する前に、システムの全体的なパフォーマンスをテストします。

## <a name="examples"></a>例  

次の例では、割り当て係数を 4 に設定します。

```tsql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO 
sp_configure 'ADR Preallocation Factor', 4;
RECONFIGURE;
GO
```

## <a name="see-also"></a>参照  

- [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [データベース復旧の高速化](../../relational-databases/accelerated-database-recovery-concepts.md)
- [高速データベース復旧の管理](../../relational-databases/accelerated-database-recovery-management.md)