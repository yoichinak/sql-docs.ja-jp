---
description: カスタム ビジネス オブジェクトの登録
title: カスタムビジネスオブジェクトの登録 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: rothja
ms.author: jroth
ms.openlocfilehash: fc5e30aef0162ecc2ffe9016e14fdfa36644aca5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724883"
---
# <a name="registering-a-custom-business-object"></a>カスタム ビジネス オブジェクトの登録
Web サーバーを使用してカスタムビジネスオブジェクト (.dll または .exe) を正常に起動するには、この手順で説明されているように、ビジネスオブジェクトの ProgID をレジストリに入力する必要があります。 この RDS 機能は、承認された実行可能ファイルのみを実行することで、Web サーバーのセキュリティを保護します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
> [!NOTE]
>  MDAC 2.0 以降および Windows DAC の場合、既定のビジネスオブジェクト [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)は、Mdac/Windows dac のインストール時に既定で登録されません。 ただし、インストール前にコンピューター上で実行するために **RDSServer DataFactory** が安全に登録されている場合は、新しいインストールのためにレジストリエントリが保持されます。  
  
### <a name="to-register-a-custom-business-object"></a>カスタムビジネスオブジェクトを登録するには:  
  
1.  [ **スタート** ] をクリックし、[ **実行**] をクリックします。  
  
2.  「 **RegEdit** 」と入力し、[ **OK]** をクリックします。  
  
3.  レジストリエディターで、 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch** レジストリキーに移動します。  
  
4.  **ADCLaunch**キーを選択し、[**編集**] メニューの [**新規作成**] をポイントし、[**キー**] をクリックします。  
  
5.  カスタムビジネスオブジェクトの ProgID を入力し、 **Enter キー**を押します。 **値**のエントリは空白のままにします。