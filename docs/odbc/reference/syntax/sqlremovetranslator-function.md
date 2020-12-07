---
description: SQLRemoveTranslator 関数
title: SQLRemoveTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92042d1a29720d8fcca32d3fb7127f24a0566b7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499605"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **Sqlremovetranslator** は、システム情報の Odbcinst.ini セクションから翻訳者に関する情報を削除し、変換プログラムのコンポーネントの使用量を1つ減らします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszTranslator*  
 代入システム情報の Odbcinst.ini キーに登録されている変換者の名前。  
  
 *lpdwUsageCount*  
 Outputこの関数が呼び出された後のトランスレーターの使用回数。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。 この関数が呼び出されたときにシステム情報にエントリが存在しない場合、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlremovetranslator**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーで、トランスレーター情報を削除できませんでした。この情報はレジストリに存在しないか、レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpsztranslator*引数が無効でした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|コンポーネントの使用状況カウントをインクリメントまたはデクリメントできませんでした|インストーラーはドライバーの使用状況カウントを減らすことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlremovetranslator** は [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) 関数を補完し、システム情報のコンポーネントの使用量を更新します。 この関数は、セットアップアプリケーションからのみ呼び出す必要があります。  
  
 **Sqlremovetranslator** は、コンポーネントの使用量を1つ減らします。 コンポーネントの使用率が0になると、システム情報の翻訳者エントリが削除されます。 Translator エントリは、システム情報の翻訳者名の下の次の場所にあります。  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **Sqlremovetranslator** は、実際にはファイルを削除しません。 呼び出し元のプログラムは、ファイルを削除し、ファイルの使用量を保持する役割を担います。 コンポーネントの使用量カウントとファイル使用量カウントの両方がゼロになった後にのみ、ファイルは物理的に削除されます。 ファイルの使用量が増加した他のアプリケーションによってファイルが使用されているかどうかによって、コンポーネント内の一部のファイルを削除したり、他のファイルを削除したりすることはできません。  
  
 **Sqlremovetranslator** は、アップグレードプロセスの一部としても呼び出されます。 アプリケーションでアップグレードを実行する必要があることが検出され、ドライバーが既にインストールされている場合は、ドライバーを削除してから再インストールする必要があります。 コンポーネントの使用量を減らすには、まず**Sqlremovetranslator**を呼び出す必要があります。その後、 **SQLInstallTranslatorEx**を呼び出して、コンポーネントの使用量カウントをインクリメントします。 アプリケーションセットアッププログラムは、古いファイルを新しいファイルに物理的に置き換える必要があります。 ファイルの使用量は変わりません。古いバージョンのファイルを使用するその他のアプリケーションでは、新しいバージョンが使用されるようになります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|トランスレーターのインストール|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
