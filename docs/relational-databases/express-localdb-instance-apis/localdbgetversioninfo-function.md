---
description: LocalDBGetVersionInfo 関数
title: LocalDBGetVersionInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6776f1ce1d5cb92bba4d570a53c95f351b501960
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542936"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 関数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  指定した SQL Server Express LocalDB バージョンの情報を返します。たとえば、存在するかどうか、LocalDB 完全バージョン番号 (ビルド番号やリリース番号を含む) などです。  
  
 この情報は、次の定義を持つ**LocalDBVersionInfo**という名前の**構造体**の形式で返されます。  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **ヘッダーファイル:** sqlncli  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>パラメーター  
 *wszVersionName*  
 [入力] LocalDB バージョンの名前。  
  
 *pVersionInfo*  
 [出力] LocalDB バージョンについての情報を格納するバッファー。  
  
 *dwVersionInfoSize*  
 代入 *VersionInfo* バッファーのサイズを保持します。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定された LocalDB バージョンが存在しません。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="details"></a>詳細  
 **構造体**のサイズ引数 (*lpVersionInfoSize*) の導入の背後にある原理は、API がさまざまなバージョンの**LocalDBVersionInfostruct**を返すことができるようにし、上位互換性と下位互換性を効果的に有効にすることです。  
  
 **構造体**のサイズ引数 (*lpVersionInfoSize*) が既知のバージョンの**LocalDBVersionInfostruct**のサイズと一致する場合、その**構造体**のバージョンが返されます。 それ以外の場合、LOCALDB_ERROR_INVALID_PARAMETER が返されます。  
  
 一般的な **LocalDBGetVersionInfo** API の使用例は次のようになります。  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>解説  
 LocalDB API を使用するコードサンプルについては、 [Localdb リファレンスの SQL Server Express](../../relational-databases/sql-server-express-localdb-reference.md)を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
