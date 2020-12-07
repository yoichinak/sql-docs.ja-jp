---
description: SQLRemoveDriverManager 関数
title: SQLRemoveDriverManager 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db880d031e803d5778c2af9b2bea08b6ed590e3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499625"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 関数
**互換性**  
 導入されたバージョン: ODBC 3.0: Windows XP Service Pack 2、Windows Server 2003 Service Pack 1、およびそれ以降のオペレーティングシステムでは非推奨となりました。  
  
 **まとめ**  
 **Sqlremovedrivermanager** は、システム情報の Odbcinst.ini エントリから ODBC コアコンポーネントに関する情報を変更または削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *pdwUsageCount*  
 Outputこの関数が呼び出された後のドライバーマネージャーの使用カウント。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。 この関数が呼び出されたときにシステム情報にエントリが存在しない場合、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlremovedrivermanager**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーは、ドライバーマネージャーの情報を削除できませんでした。レジストリに存在しないか、レジストリに見つかりませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|コンポーネントの使用状況カウントをインクリメントまたはデクリメントできませんでした|インストーラーで、ドライバーマネージャーの使用状況カウントを減らすことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlremovedrivermanager** は **sqlremovedrivermanager** 関数を補完し、システム情報のコンポーネントの使用状況を更新します。 この関数は、セットアップアプリケーションからのみ呼び出す必要があります。  
  
 **Sqlremovedrivermanager** は、コアコンポーネントの使用量カウントを1つ減らします。 コンポーネントの使用量が0になると、エントリシステム情報が削除されます。 コアコンポーネントのエントリは、システム情報の次の場所にあります ("ODBC Core" というタイトルの下)。  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  アプリケーションでは、コンポーネントの使用量とファイルの使用量がゼロになった場合に、ドライバーマネージャーファイルを物理的に削除しないでください。  
  
 **Sqlremovedrivermanager** は、実際にはファイルを削除しません。 呼び出し元のプログラムは、ファイルを削除し、ファイルの使用量のカウントを保持する役割を担います。 ただし、これらのファイルは、ファイルの使用量が増加していない他のアプリケーションによって使用されている可能性があるため、コンポーネントの使用量とファイルの使用数の両方がゼロになった場合は、ドライバーマネージャーファイルを削除しないでください。  
  
 **Sqlremovedrivermanager** は、アンインストールプロセスの一部として呼び出されます。 ODBC core コンポーネント (ドライバーマネージャー、カーソルライブラリ、インストーラー、言語ライブラリ、管理者、サンキングファイルなどが含まれます) は、全体としてアンインストールされます。 アンインストールプロセスの一部として **Sqlremovedrivermanager** を呼び出すと、次のファイルは削除されません。  

:::row:::
    :::column:::
        ODBC32DLL  
        ODBCCR32.DLL  
        ODBCCU32.DLL  
        ODBCINT.DLL  
        ODBCTRAC.DLL  
        MSVCRT40.DLL  
        ODBCCP32.CPL  
    :::column-end:::
    :::column:::
        ODBCCP32.DLL  
        ODBC16GT.DLL  
        ODBC32GT.DLL  
        DS16GT.DLL  
        DS32GT.DLL  
        ODBCAD32.EXE  
    :::column-end:::
:::row-end:::

 **Sqlremovedrivermanager** は、アップグレードプロセスの一部としても呼び出されます。 アプリケーションでアップグレードを実行する必要があることが検出され、ドライバーが既にインストールされている場合は、ドライバーを削除してから再インストールする必要があります。  
  
 コンポーネントの使用回数を減らすには、最初に**Sqlremovedrivermanager**を呼び出す必要があります。 コンポーネントの使用量を増やすには、 **Sqlinstalldriverex**を呼び出す必要があります。 アプリケーションセットアッププログラムは、古いコアコンポーネントファイルを新しいファイルに置き換える必要があります。 ファイルの使用量カウントは変わりません。また、古いバージョンのコアコンポーネントファイルを使用するその他のアプリケーションでは、新しいバージョンのファイルが使用されるようになります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーマネージャーのインストール|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
