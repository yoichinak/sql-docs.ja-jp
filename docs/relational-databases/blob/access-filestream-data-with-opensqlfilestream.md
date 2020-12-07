---
title: OpenSqlFilestream による FILESTREAM データへのアクセス | Microsoft Docs
description: OpenSqlFilestream を使用して FILESTREAM データにアクセスする方法を説明します。 この API を使用して Win32 ハンドルを取得する方法を示す例を紹介します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
apiname:
- OpenSqlFilestream
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 959bc875e314f0fbb79b51e4f9ea36dbf5414dc9
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810278"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>OpenSqlFilestream による FILESTREAM データへのアクセス
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  OpenSqlFilestream API は、ファイル システムに格納されている FILESTREAM バイナリ ラージ オブジェクト (BLOB) の Win32 互換ファイル ハンドルを取得します。 このハンドルは、次のいずれかの Win32 API に渡すことができます。[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、[WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile)、[TransmitFile](/windows/win32/api/mswsock/nf-mswsock-transmitfile)、[SetFilePointer](/windows/win32/api/fileapi/nf-fileapi-setfilepointer)、[SetEndOfFile](/windows/win32/api/fileapi/nf-fileapi-setendoffile)、[FlushFileBuffers](/windows/win32/api/fileapi/nf-fileapi-flushfilebuffers)。 このハンドルをその他の Win32 API に渡すと、ERROR_ACCESS_DENIED エラーが返されます。 このハンドルは、トランザクションをコミットまたはロールバックする前に Win32 [CloseHandle](/windows/win32/api/handleapi/nf-handleapi-closehandle) API に渡して閉じる必要があります。 ハンドルを閉じないと、サーバー側でリソースのリークが発生します。  
  
 FILESTREAM データ コンテナー アクセスはすべて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションの中で実行する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを同じトランザクションで実行することもできます。 これにより、SQL データと FILESTREAM BLOB データの一貫性が維持されます。  
  
 Win32 を使用して FILESTREAM BLOB にアクセスするには、 [Windows 認証](../../relational-databases/security/choose-an-authentication-mode.md) を有効にする必要があります。  
  
> [!IMPORTANT]  
>  ファイルを書き込みアクセス用に開くと、トランザクションは FILESTREAM エージェントによって所有されます。 トランザクションが解放されるまで、Win32 ファイル I/O だけが許可されます。 トランザクションを解放するには、書き込みハンドルを閉じる必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
HANDLE OpenSqlFilestream (  
    LPCWSTR FilestreamPath,  
    SQL_FILESTREAM_DESIRED_ACCESS DesiredAccess,  
    ULONG OpenOptions,  
    LPBYTE FilestreamTransactionContext,  
    SIZE_T FilestreamTransactionContextLength,  
    PLARGE_INTEGER AllocationSize);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *FilestreamPath*  
 [in] **PathName** 関数から返される [nvarchar(max)](../../relational-databases/system-functions/pathname-transact-sql.md) パスです。 PathName は、FILESTREAM のテーブルおよび列に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SELECT または UPDATE の権限を持つアカウントのコンテキストから呼び出す必要があります。  
  
 *DesiredAccess*  
 [in] FILESTREAM BLOB データへのアクセスに使用するモードを設定します。 この値は [DeviceIoControl 関数](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)に渡されます。  
  
|名前|値|意味|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|ファイルからデータを読み取ることができます。|  
|SQL_FILESTREAM_WRITE|1|ファイルにデータを書き込むことができます。|  
|SQL_FILESTREAM_READWRITE|2|ファイルに対してデータを読み書きできます。|  
  
> [!NOTE]  
>  これらの値は、sqlncli.h の SQL_FILESTREAM_DESIRED_ACCESS 列挙で定義されます。  
  
 *OpenOptions*  
 [in] ファイルの属性とフラグです。 このパラメーターでは、次のフラグを任意に組み合わせて指定することもできます。  
  
|フラグ|値|意味|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|特にオプションを指定せずにファイルが開かれるか、または作成されます。|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|非同期 I/O 用にファイルが開かれるか、または作成されます。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|システム キャッシュを使用せずにファイルが開かれます。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|中間キャッシュを使用せずに 直接ディスクに書き込みます。|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|ファイルが先頭から末尾まで順次アクセスされます。 システムはこれをヒントとしてファイルのキャッシュを最適化します。 アプリケーションがランダム アクセスのファイル ポインターを移動させると、最適なキャッシングが行われなくなる場合があります。|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|ファイルがランダムにアクセスされます。 システムはこれをヒントとしてファイルのキャッシュを最適化します。|  
  
 *FilestreamTransactionContext*  
 [in] [GET_FILESTREAM_TRANSACTION_CONTEXT](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) 関数から返される値です。  
  
 *FilestreamTransactionContextLength*  
 [in] GET_FILESTREAM_TRANSACTION_CONTEXT 関数から返される **varbinary(max)** データのバイト数です。 この関数は、N バイトの配列を返します。 N は関数によって決まる、返されるバイト配列のプロパティです。  
  
 *AllocationSize*  
 [in] データ ファイルの初期割り当てサイズをバイト単位で指定します。 読み取りモードでは無視されます。 このパラメーターには NULL を指定できます。その場合、ファイル システムの既定の動作が使用されます。  
  
## <a name="return-value"></a>戻り値  
 この関数の実行が成功した場合の戻り値は、指定したファイルへのオープン ハンドルです。 失敗した場合の戻り値は、INVALID_HANDLE_VALUE です。 詳細なエラー情報を取得するには、GetLastError() を呼び出します。  
  
## <a name="examples"></a>例  
 `OpenSqlFilestream` API を使用して Win32 ハンドルを取得する方法を次の例に示します。  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/access-filestream-data-w_0_1.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/access-filestream-data-w_0_2.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/access-filestream-data-w_0_3.cpp)]  
  
## <a name="remarks"></a>解説  
 この API を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client をインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント ツールとともにインストールされます。 詳細については、「 [SQL Server Native Client のインストール](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [FILESTREAM データの部分的な更新](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)   
 [FILESTREAM アプリケーションでのデータベース操作との競合の回避](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
