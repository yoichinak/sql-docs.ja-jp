---
description: SqlErrorLogEvent クラス
title: SqlErrorLogEvent クラス
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e106fa85ac8832782c339b115969e2ca8d4fad4
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891532"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent クラス
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]
  指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイル内のイベントの表示に関するプロパティを提供します。  
  
## <a name="syntax"></a>構文  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>Properties  
 SQLErrorLogEvent クラスは、次のプロパティを定義します。  
  
| プロパティ | 説明 |
| -------- | ----------- |
|FileName|データ型: **文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> エラー ログ ファイルの名前です。|  
|InstanceName|データ型: **文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> 修飾子: キー<br /><br /> ログ ファイルが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|LogDate|データ型: **datetime**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> 修飾子: キー<br /><br /> <br /><br /> イベントがログ ファイルに記録された日時。|  
|Message|データ型: **文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> イベント メッセージ。|  
|ProcessInfo|データ型: **文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> イベントのソース サーバー プロセス ID (SPID) に関する情報。|  
  
## <a name="remarks"></a>解説  
  
| Type | 名前 |
| ---- | ---- |
|MOF|Sqlmgmproviderxpsp2up.mof|  
|[DLL]|Sqlmgmprovider.dll|  
|名前空間|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>例  
 次の例では、指定したログ ファイルに記録されたすべてのイベントの値を取得する方法を示します。 この例を実行するには、を \<*Instance_Name*> のインスタンスの名前 (' Instance1 ' など) に置き換え、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ' File_Name ' をエラーログファイルの名前 (' log. 1 ' など) に置き換えます。  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>説明  
 WQL ステートメントで *InstanceName* または *FileName* が指定されていない場合、クエリは既定のインスタンスと現在のログファイルに関する情報を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 たとえば、次の WQL ステートメントは、既定のインスタンス (MSSQLSERVER) 上の現在のログ ファイル (ERRORLOG) に含まれるすべてのログ イベントを返します。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>セキュリティ  
 WMI を使用してログファイルに接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ローカルコンピューターとリモートコンピューターの両方に対して次のアクセス許可を持っている必要があります。  
  
-   **Root\Microsoft\SqlServer\ComputerManagement10** WMI 名前空間への読み取りアクセス。 既定では、すべてのユーザーがアカウントの有効化権限による読み取りアクセスを持ちます。  
  
-   エラー ログを格納したフォルダーへの読み取り権限。 既定では、エラーログは次のパスにあり \<*Drive> ます (* は、がインストールされているドライブを表し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<*InstanceName*> はのインスタンスの名前です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )。  
  
     ** \<Drive> : Server\MSSQL13** **。 \<InstanceName>\MSSQL\Log**  
  
 ファイアウォール経由で接続する場合は、リモート ターゲット コンピューターのファイアウォールで WMI 用に例外が設定されていることを確認する必要があります。 詳細については、「 [Windows Vista 以降で WMI にリモート接続する](/windows/win32/wmisdk/connecting-to-wmi-remotely-starting-with-vista)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SqlErrorLogFile クラス](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [オフライン ログ ファイルの表示](../../relational-databases/logs/view-offline-log-files.md)  
  
