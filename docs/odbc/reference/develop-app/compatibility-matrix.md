---
description: 互換性マトリックス
title: 互換性マトリックス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bafe3d85e1f4dc1c18acb057fe8c00e4ca0b36d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461564"
---
# <a name="compatibility-matrix"></a>互換性マトリックス
次の表では、このセクションで定義したアプリケーションとドライバーの種類の互換性について説明します。  
  
|アプリケーションの種類<br /><br /> およびバージョン|32ビット ODBC<br /><br /> *2.x* 2.x ドライバー|ODBC *3.x*<br /><br /> ドライバー|ODBC 3.8 ドライバー|ISO とオープングループに準拠しているドライバー|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16ビットアプリケーション、すべてのバージョン|互換性あり|互換性あり|互換性あり|互換性あり|  
|Pure *2.x* アプリケーション|互換性あり|互換性あり|互換性あり|互換性がありません [3]|  
|純粋 *2. x* 再コンパイルアプリケーション|互換性あり|互換性 [1]|互換性 [1]|互換性がありません [3]|  
|純粋 *2. x* Unicode アプリケーション|互換性あり|互換性 [1]|互換性 [1]|互換性がありません [3]|  
|純粋なオープングループおよび ISO 準拠アプリケーション|互換性なし|互換性 [2]|互換性 [2]|互換性 [2]|  
|Pure 3.0 アプリケーション|互換性なし|互換性あり|互換性あり|互換性がありません [4]|  
|Pure 3.5 アプリケーション|互換性なし|互換性あり|互換性あり|互換性がありません [4]|  
|純粋 3.8 (またはそれ以降) のアプリケーション|互換性がありません [5]|互換性がありません [5]|互換性あり|互換性がありません [4]|  
|置換されたアプリケーション|互換性あり|互換性あり|互換性あり|互換性がありません [3]|  
  
 [1] アプリケーションは、UNICODE オプション (Unicode アプリケーションの場合) を使用して ODBC 3.5 (またはそれ以降) のヘッダーを使用して再コンパイルし、ODBCVER を0x0250 に設定する必要があります。  
  
 [2] アプリケーションは ODBC 3.5 (またはそれ以降) のヘッダーを使用してコンパイルし、ODBC ドライバーマネージャーとリンクする必要があります。 また、ヘッダーフラグ ODBC_STD も設定する必要があります。  
  
 [3] この構成は、ブックマークなどの標準に含まれてい *ない ODBC 2.x* の機能があるため、正常に動作しない可能性があります。  
  
 [4] この構成は、ブックマークなどの標準に含まれてい *ない ODBC 3.x* の機能があるため、機能しない可能性があります。  
  
 [5] odbc のドライバー固有の [C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)など、odbc 2.x または2.x ドライバーに含まれていない odbc 3.8 の機能があるため、この構成は失敗する可能性があります。  
  
## <a name="driver-manager-compatibility"></a>ドライバーマネージャーの互換性  
 すべての Driver Manager バージョンで動作する必要がある ODBC 3.0 アプリケーションは、起動時に次の操作を行う必要があります。  
  
-   環境ハンドルを割り当てます。  
  
-   SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC3_80 に設定します。 ドライバーマネージャーが SQL_ERROR を返した場合、ドライバーマネージャーは3.8 より前になります。 SQL_ATTR_ODBC_VERSION を、ドライバーマネージャーに対応するように、必要に応じて SQL_OV_ODBC3 または SQL_OV_ODBC2 にリセットします。  
  
-   接続ハンドルを割り当てます。  
  
-   接続を確立します。  
  
-   SQL_DRIVER_ODBC_VER に対して SQLGetInfo を呼び出して、ドライバーのバージョンを確認します。 ドライバーが ODBC 3.8 ドライバーの場合は、ドライバー固有の C 型を使用できます。 それ以外の場合は、ドライバー固有の C データ型を使用しないでください。  
  
 再コンパイルされた ODBC 3.x アプリケーションでは、SQL_ATTR_ODBC_VERSION の SQL_OV_ODBC3_80 を指定せずに、ドライバー固有の C 型以外の ODBC 3.8 機能を使用できることに注意してください。 これは、ODBC 2.x 機能を使用した、再コンパイルされた ODBC 2.x アプリケーションと似ています。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>すべてのドライバーマネージャーと互換性のあるアプリケーションでの SQLCancelHandle の使用  
 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)は、windows 7 より前にリリースされたドライバーマネージャーではサポートされていないため、 **sqlcancelhandle**を直接呼び出すと、以前のバージョンの windows ではアプリケーションを読み込むことができません。 すべてのバージョンのドライバーマネージャーを操作し、新しいバージョンの Windows で**Sqlcancelhandle**を使用するには、アプリケーションで**LoadLibrary**と GetProcAddress を使用して、 **sqlcancelhandle**を間接的に呼び出す必要があり**ます。**  
  
## <a name="see-also"></a>参照  
 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
