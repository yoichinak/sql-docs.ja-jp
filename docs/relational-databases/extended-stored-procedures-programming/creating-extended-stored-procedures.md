---
description: 拡張ストアド プロシージャの作成
title: 拡張ストアドプロシージャの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
ms.openlocfilehash: 59a83b935549d1fdf856b61a41b6bc7727b177b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424184"
---
# <a name="creating-extended-stored-procedures"></a>拡張ストアド プロシージャの作成
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 拡張ストアド プロシージャは、次に示すプロトタイプを備えた関数です。  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 プレフィックス xp_ は省略可能です。 拡張ストアド プロシージャ名は、サーバーにインストールされたコード ページや並べ替え順に関係なく、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでの参照時には常に大文字と小文字が区別されます。 DLL を作成する際は、次の点に注意します。  
  
-   エントリ ポイントが必要である場合は、DllMain 関数を記述します。  
  
     この関数は省略可能です。ソース コードに記述されていない場合は、コンパイラにより独自のバージョン (何も実行せずに TRUE を返す) がリンクされます。 DllMain 関数を記述した場合は、スレッドまたは処理が DLL にアタッチされる際、または DLL からデタッチされる際に、オペレーティング システムによってこの関数が呼び出されます。  
  
-   DLL 外部から呼び出す関数 (拡張ストアド プロシージャ関数) はすべて、エクスポートする必要があります。  
  
     関数をエクスポートするには、.def ファイルの [エクスポート] セクションで名前を指定します。または、ソースコード内の関数名の前に、Microsoft コンパイラ拡張機能 ( \_ _declspec () が2つのアンダースコアで始まることに注意してください) を __declspec します。  
  
 拡張ストアド プロシージャ DLL を作成するには、次のファイルが必要です。  
  
|ファイル|説明|  
|----------|-----------------|  
|Srv.h|拡張ストアド プロシージャ API ヘッダー ファイル|  
|Opends60.lib|Opends60.dll のインポート ライブラリ|  
  
 拡張ストアド プロシージャ DLL を作成するには、ダイナミック リンク ライブラリ プロジェクトを作成します。 DLL の作成に関する詳細については、開発環境のドキュメントを参照してください。  
  
 すべての拡張ストアド プロシージャ DLL で次の関数を実装およびエクスポートすることを強くお勧めします。  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport) は Microsoft 固有のコンパイラ拡張子です。 お使いのコンパイラでこのディレクティブがサポートされない場合は、DEF ファイルの EXPORTS セクションでこの関数をエクスポートする必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がトレースフラグ-T260 を使用して起動された場合、またはシステム管理者特権を持つユーザーが DBCC TRACEON (260) を実行していて、拡張ストアドプロシージャ dll で __GetXpVersion () がサポートされていない場合、警告メッセージ (エラー 8131: 拡張ストアドプロシージャ dll '% ' はエクスポート \_ _GetXpVersion ()) がエラーログに出力され ( \_ _GetXpVersion () は、2つのアンダースコアで始まります)。  
  
 拡張ストアド プロシージャ DLL により __GetXpVersion() がエクスポートされ、この関数によって返されるバージョンがサーバーで要求されるバージョンよりも低い場合、この関数によって返されたバージョンとサーバーが必要とするバージョンを示す警告メッセージがエラー ログに出力されます。 このメッセージが表示された場合は、_GetXpVersion () から正しくない値が返され \_ ているか、以前のバージョンの srv.sys を使用してコンパイルしています。  
  
> [!NOTE]  
>  拡張ストアド プロシージャでは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 関数 SetErrorMode を呼び出さないでください。  
  
 実行時間の長い拡張ストアド プロシージャの場合は、srv_got_attention を定期的に呼び出すことにより、接続が強制的に切断された場合やバッチが中断された場合に、その拡張ストアド プロシージャが自身を終了できるようにすることをお勧めします。  
  
 拡張ストアド プロシージャ DLL をデバッグするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn ディレクトリにその拡張ストアド プロシージャをコピーします。 デバッグセッションの実行可能ファイルを指定するには、実行可能ファイルのパスとファイル名を入力し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます (たとえば、C:\PROGRAM の SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe)。 Sqlservr.exe 引数の詳細については、「 [Sqlservr.exe アプリケーション](../../tools/sqlservr-application.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [srv_got_attention &#40;拡張ストアドプロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
