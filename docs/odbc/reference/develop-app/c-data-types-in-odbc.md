---
description: ODBC の C データ型
title: ODBC の C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395f60860dd3179326687a6c2fb10bbaf027ca3a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494762"
---
# <a name="c-data-types-in-odbc"></a>ODBC の C データ型
ODBC では、アプリケーション変数とそれに対応する型識別子によって使用される C データ型を定義します。 これらは、結果セットの列およびステートメントのパラメーターにバインドされるバッファーによって使用されます。 たとえば、アプリケーションが文字形式で結果セットの列からデータを取得するとします。 SQLCHAR * データ型の変数を宣言し、この変数を SQL_C_CHAR の型識別子を使用して結果セット列にバインドします。 C データ型と型識別子の完全な一覧については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。  
  
 ODBC では、各 SQL データ型から C データ型への既定のマッピングも定義されています。 たとえば、データソース内の2バイトの整数は、アプリケーションの2バイトの整数にマップされます。 既定のマッピングを使用するには、アプリケーションで SQL_C_DEFAULT の種類の識別子を指定します。 ただし、相互運用性の理由から、この識別子の使用は推奨されていません。  
  
 ODBC 1.x で定義 *されて* いるすべての整数 C データ型が署名されています。 署名されていない C データ型と、それに対応する型識別子が ODBC 2.0 で追加されました。 このため、アプリケーションとドライバーは *、1.x バージョンを扱う* ときに特に注意する必要があります。  
  
## <a name="c-data-type-extensibility"></a>C データ型の拡張性  
 ODBC 3.8 では、ドライバー固有の C データ型を指定できます。 これにより、 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)、または [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)を呼び出すと、ODBC アプリケーションで SQL 型をドライバー固有の C 型としてバインドできます。 これは、既存の C データ型が新しいサーバーのデータ型を正しく表していない可能性があるため、新しいサーバーの種類をサポートする場合に便利です。 ドライバー固有の C 型を使用すると、ドライバーによって実行される変換の数を増やすことができます。  
  
 たとえば、データベース管理システム (DBMS) で、日付と時刻をタイムゾーン情報で表す新しい SQL 型 **DATETIMEOFFSET**が導入されたとします。 ODBC には、 **DATETIMEOFFSET**をこれする特定の C 型はありません。 アプリケーションでは、 **DATETIMEOFFSET** を SQL_C_BINARY としてバインドし、ユーザー定義データ型にキャストする必要があります。 ODBC 3.8 以降では、C データ型の拡張性があり、ドライバーは、対応する新しい C 型を定義できます。 たとえば、新しい SQL 型 DATETIMEOFFSET の場合、ドライバーは、SQL_C_DATETIMEOFFSET などの新しい対応する C 型を定義できます。 次に、アプリケーションは、新しい SQL 型をドライバー固有の C 型としてバインドできます。  
  
 次のように、ドライバーで C データ型が定義されます。  
  
-   アプリケーション、ODBC ドライバー、およびドライバーマネージャーの ODBC 対応レベルは 3.8 (またはそれ以降) です。  
  
-   ドライバー固有の C 型のデータ範囲は、0x4000 とになります。  
  
-   ドライバーは、C 型に対応するデータの構造を定義します。  これは、ドライバー固有の SDK で行うことができます。  
  
 ドライバーマネージャーは、0x4000 との範囲で定義されている C 型を検証しません。ドライバーは、検証と任意のデータ型変換を実行します。 ただし、ドライバーマネージャーに渡された C 型のデータ範囲が0x0000 から0x3FFF の場合、または 0x8000 ~ 0xFFFF の場合は、ドライバーマネージャーによって C データ型が検証されます。  
  
> [!NOTE]  
>  ドライバー固有の C データ型については、ドライバーのドキュメントを参照してください。  
  
 3.8 の ODBC コンプライアンスレベルを指定するには、アプリケーションは、SQL_ATTR_ODBC_VERSION 属性を**SQL_OV_ODBC3_80**に設定して[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)を呼び出します。 アプリケーションでは、ドライバーのバージョンを確認するために、SQL_DRIVER_ODBC_VER で **SQLGetInfo** を呼び出します。  
  
 ODBC 3.8 の詳細については、「 [odbc 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)
