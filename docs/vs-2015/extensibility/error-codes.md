---
title: エラーコード |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fef596fdfa9bb29fac38c72890392c33a86b31d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204559"
---
# <a name="error-codes"></a>エラー コード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソース管理プラグイン API 関数からエラーが返された場合、次のエラーコードのいずれかである必要があります。 すべてのエラーは負、警告、または情報エラーコードは正の値であり、成功は0です。  
  
|エラー コード|値|説明|  
|----------------|-----------|-----------------|  
|`SCC_I_SHARESUBPROJOK`|7|プラグインでは、2つの手順でソース管理からのファイルの追加がサポートされています。 詳細については、「 [Sccsetoption](../extensibility/sccsetoption-function.md)」を参照してください。|  
|`SCC_I_FILEDIFFERS`|6|ローカルファイルがソース管理データベースのファイルと異なります (たとえば、 [Sccdiff](../extensibility/sccdiff-function.md) はこの値を返す可能性があります)。|  
|`SCC_I_RELOADFILE`|5|ソース管理操作中にローカルファイルが変更されました。可能な場合は、IDE によってファイルが再読み込みされます。|  
|`SCC_I_FILENOTAFFECTED`|4|ファイルは影響を受けません。|  
|`SCC_I_PROJECTCREATED`|3|プロジェクトは、ソース管理操作中に作成されました (たとえば、フラグが指定されている場合は [Sccopenproject](../extensibility/sccopenproject-function.md) の呼び出し中 `SCC_OP_CREATEIFNEW` )。|  
|`SCC_I_OPERATIONCANCELED`|2|操作が取り消されました。|  
|`SCC_I_ADV_SUPPORT`|1|プラグインは、指定されたコマンドの詳細オプションをサポートしています。 詳細については、「 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)」を参照してください。|  
|`SCC_OK`|0|正常終了しました。|  
|`SCC_E_INITIALIZEFAILED`|-1|エラー: 初期化に失敗しました。|  
|`SCC_E_UNKNOWNPROJECT`|-2|エラー: プロジェクトが不明です。|  
|`SCC_E_COULDNOTCREATEPROJECT`|-3|エラー: プロジェクトを作成できませんでした。|  
|`SCC_E_NOTCHECKEDOUT`|-4|エラー: ファイルはチェックアウトされていません。|  
|`SCC_E_ALREADYCHECKEDOUT`|-5|エラー: ファイルは既にチェックアウトされています。|  
|`SCC_E_FILEISLOCKED`|-6|エラー: ファイルはロックされています。|  
|`SCC_E_FILEOUTEXCLUSIVE`|-7|エラー: ファイルは排他的にチェックアウトされています。|  
|`SCC_E_ACCESSFAILURE`|-8|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|  
|`SCC_E_CHECKINCONFLICT`|-9|エラー: チェックイン中に競合が発生しました。|  
|`SCC_E_FILEALREADYEXISTS`|-10|エラー: ファイルは既に存在します。|  
|`SCC_E_FILENOTCONTROLLED`|-11|エラー: ファイルがソース管理下にありません。|  
|`SCC_E_FILEISCHECKEDOUT`|-12-01.2.2|エラー: ファイルはチェックアウトされています。|  
|`SCC_E_NOSPECIFIEDVERSION`|-13|エラー: 指定されたバージョンがありません。|  
|`SCC_E_OPNOTSUPPORTED`|-14|エラー: 操作はサポートされていません。|  
|`SCC_E_NONSPECIFICERROR`|checks.-15-minutes|不特定のエラーです。|  
|`SCC_E_OPNOTPERFORMED`|-16|エラー。操作は実行されませんでした。|  
|`SCC_E_TYPENOTSUPPORTED`|-17|エラー: ファイルの種類 (バイナリなど) は、ソースコード管理システムではサポートされていません。|  
|`SCC_E_VERIFYMERGE`|-18|ファイルは自動マージされていますが、ユーザーの確認が保留中であるため、チェックされていません。|  
|`SCC_E_FIXMERGE`|-19|ファイルは自動マージされていますが、マージの競合が原因でチェックインされていないため、手動で解決する必要があります。|  
|`SCC_E_SHELLFAILURE`|-20|シェルエラーによりエラーが発生しています。|  
|`SCC_E_INVALIDUSER`|-21|エラー: ユーザーが無効です。|  
|`SCC_E_PROJECTALREADYOPEN`|-22|エラー: プロジェクトは既に開いています。|  
|`SCC_E_PROJSYNTAXERR`|-23|プロジェクトの構文エラーです。|  
|`SCC_E_INVALIDFILEPATH`|-24|エラー: ファイルパスが無効です。|  
|`SCC_E_PROJNOTOPEN`|-25|エラー: プロジェクトが開いていません。|  
|`SCC_E_NOTAUTHORIZED`|-26|エラー: ユーザーにはこの操作を実行する権限がありません。|  
|`SCC_E_FILESYNTAXERR`|-27|ファイルの構文エラーです。|  
|`SCC_E_FILENOTEXIST`|-28-preview|エラー。ローカルファイルが存在しません。|  
|`SCC_E_CONNECTIONFAILURE`|-29|エラー: 接続エラーが発生しました。|  
|`SCC_E_UNKNOWNERROR`|-30|不明なエラー。|  
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|バックグラウンドの取得操作が現在進行中です。|  
  
## <a name="macros-provided-for-quick-checking"></a>クイックチェック用のマクロ  
  
```cpp#  
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)  
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)  
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)  
```  
  
## <a name="remarks"></a>注釈  
 引数として渡されたローカルファイルが作業フォルダーに存在しない場合、すべてのソース管理プラグイン API 関数 ( [Sccadd](../extensibility/sccadd-function.md)、 [Sccadd](../extensibility/scccheckin-function.md)、 [sccadd](../extensibility/sccdiff-function.md)を除く) が成功することが期待されます。 たとえば、IDE は、作業フォルダーに存在しないがソース管理システムに存在するファイルに対して、 [Scccheckout](../extensibility/scccheckout-function.md) または [SccUncheckout](../extensibility/sccuncheckout-function.md) への呼び出しを発行する場合があります。 この呼び出しは成功します。 作業フォルダーまたはソース管理システムにファイルが存在しない場合にのみ、関数は失敗します。  
  
 やなどの特定の関数は、 `SccAdd` `SccCheckin` `SCC_E_FILENOTEXIST` 作業フォルダー内のファイルが存在しない場合に、を返す必要があります。 関数がソース管理システムの有効なファイル名で動作する場合、作業ファイルが存在しないときには、他の関数が成功すると想定されます。  
  
 ソース管理プラグインは、操作中にプラグインがファイルを読み取り専用としてマークしていた場合でも、作業フォルダー内のファイルに対する権限についての仮定を行いません。 作業フォルダー内のファイルは、プラグインのコントロールの外部で移動、削除、および変更できます。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
