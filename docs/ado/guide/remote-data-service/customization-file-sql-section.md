---
description: カスタマイズ ファイルの SQL セクション
title: カスタマイズファイル SQL Section |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: rothja
ms.author: jroth
ms.openlocfilehash: d17fa12aa0b07b265fb8f26b6ac1b6c584015d1e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724763"
---
# <a name="customization-file-sql-section"></a>カスタマイズ ファイルの SQL セクション
**Sql**セクションには、クライアントのコマンド文字列を置き換える新しい sql 文字列を含めることができます。 セクションに SQL 文字列がない場合、セクションは無視されます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 新しい SQL 文字列を *パラメーター化*することができます。 つまり、 **sql** セクションの sql 文字列 ('? ' 文字で指定された) のパラメーターは、クライアントのコマンド文字列内の *識別子* 内の対応する引数に置き換えることができます (かっこで囲まれたコンマ区切りのリストで指定されます)。 識別子と引数リストは関数呼び出しのように動作します。  
  
 たとえば、クライアントのコマンド文字列がで、 `"CustomerByID(4)"` sql section ヘッダーがで、 `[SQL CustomerByID]` 新しい sql section 文字列がハンドラーによって生成され、 `"SELECT * FROM Customers WHERE CustomerID = ?".` その文字列を使用してデータソースにクエリを実行するとし `"SELECT * FROM Customers WHERE CustomerID = 4"` ます。  
  
 新しい SQL ステートメントが null 文字列 ("") の場合、セクションは無視されます。  
  
 新しい SQL ステートメント文字列が有効でない場合、ステートメントの実行は失敗します。 クライアントパラメーターは事実上無視されます。 次のように指定して、クライアントのすべての SQL コマンドを無効にすることができます。  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>構文  
 代替の SQL 文字列エントリの形式は次のとおりです。  
  
 **SQL =**   
 ***sqlString***  
  
|要素|説明|  
|----------|-----------------|  
|**SQL**|これが SQL セクションエントリであることを示すリテラル文字列。|  
|***sqlString***|クライアント文字列を置き換える SQL 文字列。|  
  
## <a name="see-also"></a>参照  
 [カスタマイズファイルの接続セクション](./customization-file-connect-section.md)   
 [カスタマイズファイルログセクション](./customization-file-logs-section.md)   
 [カスタマイズファイルの UserList セクション](./customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](./datafactory-customization.md)   
 [必要なクライアント設定](./required-client-settings.md)   
 [カスタマイズファイルについて](./understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](./writing-your-own-customized-handler.md)