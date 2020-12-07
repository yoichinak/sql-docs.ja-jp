---
description: SQLInstallDriverManager 関数
title: SQLInstallDriverManager 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b39e2c9304fd47394617d48f22ac91284af1b45d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421176"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 関数
**互換性**  
 導入されたバージョン: ODBC 1.0: Windows XP Service Pack 2、Windows Server 2003 Service Pack 1、およびそれ以降のオペレーティングシステムでは非推奨となりました。  
  
 **まとめ**  
 **Sqlinstalldrivermanager** は、ODBC core コンポーネントのインストール先ディレクトリのパスを返します。 呼び出し元のプログラムは、実際にはドライバーマネージャーのファイルをターゲットディレクトリにコピーする必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引数  
 *lpszPath*  
 Outputインストール先ディレクトリのパス。  
  
 *cbPathMax*  
 代入 *Lpszpath*の長さ。 これは、少なくとも _MAX_PATH バイトである必要があります。  
  
 *pcbPathOut*  
 Output *Lpszpath*で返された合計バイト数 (null 終端バイトを除く)。 返すことのできるバイト数が *Cbpathmax*以上の場合、 *lpszpath* 内のパスは *cbpathmax* から null 終端文字に切り捨てられます。 *Pcbpathout*引数は null ポインターにすることができます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlinstalldrivermanager**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszpath*引数は、出力パスを格納するのに十分な大きさではありませんでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *Cbpathmax*引数が _MAX_PATH 未満でした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|コンポーネントの使用状況カウントをインクリメントまたはデクリメントできませんでした|インストーラーで、ODBC コアコンポーネントの使用回数を増やすことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlinstalldrivermanager** が呼び出され、ODBC コアコンポーネントのパスが返され、システム情報に含まれるコンポーネントの使用量が増加します。 ドライバーマネージャーのバージョンが既に存在していても、そのドライバーのコンポーネントの使用量が存在しない場合、新しいコンポーネントの使用状況のカウント値は2に設定されます。  
  
 アプリケーションのセットアッププログラムでは、コアコンポーネントファイルを物理的にコピーし、ファイルの使用量のカウントを維持する必要があります。 コアコンポーネントファイルが事前にインストールされていない場合は、アプリケーションセットアッププログラムによってファイルがコピーされ、ファイルの使用量が作成されます。 ファイルが既にインストールされている場合、セットアッププログラムは単にファイルの使用量をインクリメントします。  
  
 以前のバージョンのドライバーマネージャーがアプリケーションセットアッププログラムによって既にインストールされている場合は、コアコンポーネントの使用回数が有効になるように、コアコンポーネントをアンインストールしてから再インストールする必要があります。 コンポーネントの使用回数を減らすには、最初に**Sqlremovedrivermanager**を呼び出す必要があります。 コンポーネントの使用量を増やすには、 **Sqlinstalldrivermanager**を呼び出す必要があります。 アプリケーションセットアッププログラムは、古いコアコンポーネントファイルを新しいファイルに置き換える必要があります。 ファイルの使用量カウントは変わりません。また、古いバージョンのコアコンポーネントファイルを使用する他のアプリケーションでは、新しいバージョンのファイルが使用されるようになります。  
  
 ODBC のコアコンポーネント、ドライバー、およびトランスレーターの新規インストールでは、アプリケーションセットアッププログラムは、 **Sqlinstalldrivermanager**、 **sqlinstalldrivermanager**、 **Sqlconfigdriver** ( *frequest* for ODBC_INSTALL_DRIVER) の順に、次の関数を呼び出す必要が**あります。** コアコンポーネント、ドライバー、およびトランスレーターのアンインストールでは、アプリケーションセットアッププログラムは、 **Sqlremovetranslator**、 **sqlremovetranslator**、 **sqlremovedrivermanager**の順に次の関数を呼び出す必要があります。 これらの関数は、この順序で呼び出す必要があります。 すべてのコンポーネントをアップグレードする場合は、すべてのアンインストール機能を順番に呼び出し、すべてのインストール機能を順番に呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーの追加、変更、または削除|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|ドライバーのインストール|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|トランスレーターのインストール|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|ドライバーの削除|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|ドライバーマネージャーの削除|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|トランスレーターの削除|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
