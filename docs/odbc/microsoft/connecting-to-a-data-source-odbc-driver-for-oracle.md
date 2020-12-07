---
description: データ ソース (ODBC Driver for Oracle) への接続
title: データソースへの接続 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6951dd89f3ad1a311d93aca460c61dc7317b2f30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483665"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>データ ソース (ODBC Driver for Oracle) への接続
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 ODBC アプリケーションは、さまざまな方法で接続情報を渡すことができます。 たとえば、アプリケーションでは、ドライバーが常にユーザーに接続情報の入力を求めることがあります。 または、データソース接続を指定する接続文字列がアプリケーションで想定されている場合があります。 データソースへの接続方法は、ODBC アプリケーションで使用される接続方法によって異なります。  
  
 データソースに接続する一般的な方法の1つは、[データソース] ダイアログボックスを使用することです。 ODBC アプリケーションがダイアログボックスを使用するように設定されている場合は、そのダイアログボックスが表示され、適切なデータソース接続情報を入力するように求められます。  
  
 [接続文字列](../../odbc/microsoft/connection-string-format-and-attributes.md)を使用してデータソースに接続することもできます。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>ダイアログボックスを使用してデータソースに接続するには  
  
1.  [データソース] ダイアログボックスが表示されたら、Oracle データソースを選択し、[OK] をクリックします。 ［接続］ダイアログ ボックスが表示されます。  
  
2.  [接続] ダイアログボックスに適切な情報を入力し、[OK] をクリックします。  
  
 接続情報が検証されると、アプリケーションは ODBC Driver for Oracle を使用して、データソースに含まれている情報にアクセスできます。
