---
description: 管理プログラム
title: 管理プログラム |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5aef5e00fa69fd1f699228b2c0ac82b2a8041962
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429034"
---
# <a name="administration-program"></a>管理プログラム
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 ODBC 管理者である管理プログラムは、Windows SDK/MDAC SDK に含まれています。 このプログラムとは、SDK のユーザーが再配布できます。 さらに、開発者は独自の管理プログラムを作成できます。 通常、開発者は、データソースの構成を完全に制御する必要がある場合、または管理プログラムとして機能するアプリケーションからデータソースを直接構成する場合にのみ、独自の管理プログラムを作成します。 たとえば、スプレッドシートプログラムでは、ユーザーが実行時にデータソースを追加して使用できるようにすることができます。  
  
 管理プログラムは、最初にインストーラー DLL を読み込みます。 次に、インストーラー DLL 内の関数を呼び出して、次のタスクを実行します。  
  
-   **データソースを対話形式で追加、変更、または削除します。** 管理プログラムは、 **Sqlmanagedatasources**、 **sqlmanagedatasources**、または **sqlmanagedatasources**を呼び出すことができます。  
  
     **Sqlmanagedatasources** : ユーザーがデータソースを追加、変更、または削除したり、トレースオプションを指定したりできるダイアログボックスを表示します。この関数は、コントロールパネルからインストーラー DLL が直接呼び出されたときに呼び出されます。 **Sqlcreatedatasource** には、ユーザーがデータソースを追加できるダイアログボックスが表示されます。 **Sqlconfigdatasource** は、ドライバーのセットアップ DLL に直接呼び出しを渡します。  
  
     どのような場合でも、インストーラー DLL は、ドライバーセットアップ DLL 内の **Configdsn** を呼び出して、実際にデータソースを追加、変更、または削除します。 ドライバーセットアップ DLL により、ユーザーに追加情報の入力を求められる場合があります。  
  
-   **データソースをサイレントモードで追加、変更、または削除します。** 管理プログラムは、インストーラー DLL で **Sqlconfigdatasource** を呼び出し、null ウィンドウハンドル、追加、変更、または削除するデータソースの名前、およびレジストリの値の一覧を渡します。 インストーラー DLL は、ドライバーセットアップ DLL 内の **Configdsn** を呼び出して、実際にデータソースを追加、変更、または削除します。  
  
-   **既定のデータソースを追加、変更、または削除します。** 既定のデータソースは他のデータソースと同じですが、その名前が既定値である点が異なります。 他のデータソースと同じ方法で追加、変更、または削除されます。
