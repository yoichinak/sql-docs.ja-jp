---
description: 付録 - 1 (MySQLToSQL)
title: 付録-1 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2d22766d-ff09-420d-ae7c-13b443e28bd0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e3c86b950eb156e966db1cfe030bc40753d01f6e
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988434"
---
# <a name="appendix---1-mysqltosql"></a>付録 - 1 (MySQLToSQL)
SSMA コンソールのコマンドラインオプションのクイックビューを次に示します。  
  
|法. いいえ。|Switch|必須|スイッチ引数|許可される値|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/スクリプト|はい|scriptfile|有効な XML ファイル名です。<br /><br />コンソールスクリプト定義ファイル。|  
|2|-v/variable|いいえ|変数 valuefile|有効な XML ファイル名です。<br /><br />スクリプトファイルで変数を使用する場合は、このファイルを指定する必要があります。|  
|3|-c/serverconnection|いいえ|serverconnectionfile|有効な XML ファイル名です。<br /><br />このファイルには、サーバーの接続情報が含まれています。|  
|4|-x/xmloutput|いいえ|xmloutputfile|このオプションは、XML 形式のコンソール出力を示します。 このオプションが指定されていない場合、既定の出力はテキスト形式です。<br /><br />Xmloutputfile が指定されていない場合、XML 出力は STDOUT に送られます。<br /><br />Xmloutputfile は、コンソール出力を XML 形式で記述するファイルの名前です。|  
|5|-l/ログ|いいえ|logfile|有効なファイル名です。|  
|6|-e/projectenvironment|いいえ|project環境フォルダー|SSMA プロジェクト環境ファイルを含む有効なフォルダー名です。|  
|7|-p/securepassword|いいえ|-a/add {<server_id> [,...n] &#124; すべて}-c&#124;microsoft.sqlserver.management.common.serverconnection> <サーバー接続-ファイル> [-v&#124;variable <variable-file>] [-o/overwrite]<br /><br />or<br /><br />-a/add {<server_id> [,...n] すべての}-s&#124;スクリプトを &#124; <スクリプトファイル> [-v&#124;variable <variable-file>] [-o/overwrite]<br /><br />-r/remove {<server_id> [,...n] &#124; すべて}<br /><br />-l/リスト<br /><br />-e/export {<サーバー id> [,...n] すべてを &#124;} <暗号化されたパスワードファイル><br /><br />-i/インポート {<サーバー id> [,...n] すべてを &#124;} <暗号化されたパスワードファイル>|このオプションを指定する場合は、他のオプションと組み合わせることはできません。<br /><br />サーバー id: サーバー {string} に対して指定された一意の ID<br /><br />サーバー-接続-ファイル: サーバー定義ファイル (serverconnectionfile または scriptfile)。<br /><br />変数-値-ファイル: 変数定義ファイルで、サーバー接続ファイルで使用されます。<br /><br />暗号化-パスワードファイル: ユーザー指定のパスフレーズを使用して暗号化されたサーバーパスワードファイルです。|  
|8|-?|いいえ|適用しない|適用しない|  
  
## <a name="see-also"></a>参照  
[SSMA コンソールの実行 (MySQL)](./executing-the-ssma-console-mysqltosql.md)  
