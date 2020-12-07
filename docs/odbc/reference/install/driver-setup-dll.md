---
description: ドライバーのセットアップ DLL
title: ドライバーのセットアップ DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79fff6ce68e7860b444ebefa736cb959cd54576b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476208"
---
# <a name="driver-setup-dll"></a>ドライバーのセットアップ DLL
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 ドライバーセットアップ DLL には、 **configdriver** および **configdriver** 関数が含まれています。 **Configdriver** は、ドライバー固有の情報をレジストリに入力するなど、ドライバー固有のインストールタスクを実行します。 **Configdsn** では、データソースに関するドライバー固有の情報がレジストリに保持されます。 これらの関数の詳細については、「 [SETUP DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md)」を参照してください。  
  
 **Configdsn** は、レジストリにデータソース情報を保持するために、インストーラー DLL 内の次の関数を呼び出します。  
  
-   **Sqlwritedsntoini**。 データ ソースを追加します。  
  
-   **Sqlremovedsnfromini**。 データソースを削除します。  
  
-   **Sqlwriteprivateprofilestring**。 データソース仕様サブキーの下にドライバー固有の値を書き込みます。  
  
-   **Sqlgetprivateprofilestring**。 データソース仕様サブキーからドライバー固有の値を読み取ります。  
  
-   **Sqlgettranslator**。 ユーザーに、翻訳者の名前とオプションの入力を求めます。 この関数は、translator セットアップ DLL で **Configtranslator** を呼び出します。  
  
 ドライバーのセットアップ DLL は、ドライバーの開発者によって作成されます。 ドライバー DLL または別の DLL の一部にすることができます。
