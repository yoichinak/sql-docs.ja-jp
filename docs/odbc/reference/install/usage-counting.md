---
description: 使用状況のカウント
title: 使用量カウント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e8c02aae51c47b13970a1824e3c0c9c417eb5f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499695"
---
# <a name="usage-counting"></a>使用状況のカウント
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 コンポーネントごとに、コンポーネントの使用量と1つ以上のオプションのファイル使用量のカウントという2種類の使用量カウントがレジストリに保持されます。 コンポーネント使用量カウントは、インストーラー DLL がレジストリエントリを保持するのに役立ちます。 これは、ODBC Core、driver、および translator サブキーの下の UsageCount 値に格納されます。 UsageCount の値の形式、およびこれらのサブキーの詳細については、「 [ODBC コンポーネントのレジストリエントリ](../../../odbc/reference/install/registry-entries-for-odbc-components.md)」を参照してください。  
  
 コンポーネントが最初にインストールされると、インストーラー DLL によってサブキーが作成され、そのサブキーの UsageCount 値のデータが1に設定されます。 コンポーネントを再インストールすると、インストーラーの DLL によって使用量が増加します。 コンポーネントが削除されると、インストーラーの DLL によって使用量が減少します。 使用状況カウントが0になると、インストーラー DLL によってコンポーネントのサブキーが削除されます。  
  
> [!CAUTION]  
>  アプリケーションでは、コンポーネントの使用量とファイルの使用量がゼロになった場合に、ドライバーマネージャーファイルを物理的に削除しないでください。  
  
 ファイルの使用量カウントは、使用量の増加または減少ではなく、実際にファイルをコピーまたは削除する必要があるかどうかを判断するのに役立ちます。 ODBC コンポーネント、つまり odbc コンポーネント内のファイルは共有されており、さまざまなアプリケーションによってインストールまたは削除できるため、このことが重要になります。 コンポーネントの使用量とファイルの使用率が0になると、アプリケーションはドライバーおよびトランスレーターファイルを削除できます。 ただし、これらのファイルは、ファイルの使用量が増加していない他のアプリケーションによって使用される可能性があるので、コンポーネントの使用量とファイルの使用量の両方がゼロになった場合は、ドライバーマネージャーファイルを削除しないでください。  
  
> [!NOTE]  
>  Microsoft® WindowsNT®/windows2000 では、ファイルの使用量のカウントは省略可能です。  
  
 ファイルの使用回数は、セットアッププログラムによって、 **Sqlinstalldrivermanager**、 **sqlinstalldrivermanager**、 **SQLInstallTranslatorEx**、 **sqlinstalldrivermanager**、 **sqlremovedriver**、または **sqlremovetranslator**を呼び出した後に保持されます。  
  
 コンポーネントが最初にインストールされると、セットアッププログラムまたはインストーラー DLL によって、システムにまだ存在しないコンポーネント内のファイルごとに、次のキーの下に値が作成されます。  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  ソフトウェア  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 これらの値のデータを1に設定し、ファイルをシステムにコピーします。 コンポーネントを再インストールすると、セットアッププログラムまたはインストーラーの DLL によって使用量のカウントが増加します。 コンポーネントが削除されると、セットアッププログラムまたはインストーラー DLL によって使用量カウントが減少します。 使用量が0になると、セットアッププログラムまたはインストーラーの DLL によってそのファイルの値が削除されます。また、コンポーネントがドライバーまたは変換ツールである場合は、によってファイルが削除されます。 ドライバーマネージャーファイルは削除しないでください。  
  
 次の表に、[ファイルの使用状況のカウント] の値の形式を示します。  
  
|名前|データ型|データ|  
|----------|---------------|----------|  
|*完全パス*|REG_DWORD|*count*|  
  
 たとえば、Informix 用のドライバーで Infrmx32.dll と Infrmx32 ファイルを使用し、このドライバーが2回インストールされているとします。 Informix ドライバーの SharedDlls サブキーの下の値は、次のようになります。  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
