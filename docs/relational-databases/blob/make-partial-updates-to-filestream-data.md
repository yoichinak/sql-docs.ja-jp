---
title: FILESTREAM データの部分的な更新 | Microsoft Docs
description: FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 値を使用して FILESTREAM BLOB データを部分的に更新する方法について説明します。 部分更新の例を紹介します。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3b47cdacd079bfa1235427938b3fa214a1babeb7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809903"
---
# <a name="make-partial-updates-to-filestream-data"></a>FILESTREAM データの部分的な更新
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  アプリケーションでは、FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT を使用して FILESTREAM BLOB データを部分的に更新します。 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 関数は、この値と、 [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) から FILESTREAM ドライバーに返されるハンドルを渡します。 このドライバーによって、サーバー側の現在の FILESTREAM データが、ハンドルが参照するファイルにコピーされます。 ハンドルへの書き込みが行われた後にアプリケーションが FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 値を発行すると、最後の書き込み操作は維持され、それより前のハンドルへの書き込み操作は失われます。  
  
> [!NOTE]  
>  FILESTREAM のリモート アクセスは、 [SMB プロトコル](/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview) に依存しています。  
  
## <a name="example"></a>例  
 次の例では、 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 値を使用して、挿入された FILESTREAM BLOB を部分的に更新する方法を示します。  
  
> [!NOTE]  
>  この例では、「 [FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md) 」および「 [FILESTREAM データを格納するテーブルを作成する方法](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)」で作成した、FILESTREAM が有効なデータベースとテーブルが必要です。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## <a name="see-also"></a>参照  
 [OpenSqlFilestream による FILESTREAM データへのアクセス](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [FILESTREAM データ用のクライアント アプリケーションの作成](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
