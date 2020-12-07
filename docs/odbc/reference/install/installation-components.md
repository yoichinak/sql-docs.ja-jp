---
description: インストール コンポーネント
title: インストールコンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aac17b66b52b6d5b167f670302b8e1df14f8907a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499825"
---
# <a name="installation-components"></a>インストール コンポーネント
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 ユーザーがセットアッププログラムを実行すると、インストールプロセスが開始されます。 セットアッププログラムは、各ドライバーの *インストーラー dll* および *ドライバーセットアップ dll* と連携して動作します。 セットアッププログラムとインストーラー DLL の両方で、 **Sqlinstalldriverex** 関数と **SQLInstallTranslatorEx** 関数の引数を使用して、各コンポーネントでコピーまたは削除するファイルを決定します。 次の図は、これらのインストールコンポーネント間の関係を示しています。  
  
 ![インストール コンポーネント間の関係](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Odbc 2.x では、各 ODBC コンポーネントに必要なファイルを *記述するために odbc .inf* ファイルが使用されていますが、odbc *3. x*では使用されません。 ODBC 3.x コンポーネントを出荷するドライバーでは *、odbc .inf* ファイルを作成する必要はありません。 **Sqlinstalldriver**と**SQLInstallODBC**の削除、および**sqlinstalldriver**が廃止されたため、Odbc が不要になりました。 Odbc の Driver キーワードセクションに含まれていたドライバー情報が、 **Sqlinstalldriverex**の*lpszdriver*引数に指定されるようになりました。 Odbc の [ODBC Translator] セクションおよび Translator Specification セクションに含まれていた変換情報が、 **SQLInstallTranslatorEx**の*lpsztranslator*引数に指定されるようになりました。 これらの変更により、プラットフォーム間での ODBC インストーラーの移植性が向上します。  
  
 これらのコンポーネントの詳細については、このセクションの最後にある次のトピックを参照してください。  
  
-   [セットアップ プログラム](../../../odbc/reference/install/setup-program.md)  
  
-   [インストーラー DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [ドライバーのセットアップ DLL](../../../odbc/reference/install/driver-setup-dll.md)
