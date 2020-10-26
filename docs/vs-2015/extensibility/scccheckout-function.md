---
title: SccCheckout 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f23290ebfadd1b6e3d34f808d5ea0ccccbb3c319
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200158"
---
# <a name="scccheckout-function"></a>SccCheckout 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

完全修飾ファイル名のリストを指定した場合、この関数はローカルドライブを確認します。 コメントは、チェックアウトされているすべてのファイルに適用されます。Comment 引数には文字列を指定でき `null` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccCheckout (  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LPCSTR    lpComment,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pvContext  
 からソース管理プラグインのコンテキスト構造。  
  
 hWnd  
 からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。  
  
 nFiles  
 からチェックアウト対象として選択されたファイルの数。  
  
 lpFileNames 名  
 からチェックアウトするファイルの完全修飾ローカルパス名の配列。  
  
 lpComment  
 からチェックアウトされる選択された各ファイルに適用されるコメント。  
  
 限ら  
 からコマンドフラグ ( [特定のコマンドで使用されるビットフラグを](../extensibility/bitflags-used-by-specific-commands.md)参照)。  
  
 pvOptions  
 からソース管理プラグイン固有のオプション。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|チェックアウトに成功しました。|  
|SCC_E_FILENOTCONTROLLED|選択したファイルはソースコード管理されていません。|  
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|  
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|  
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 ファイルがチェックアウトされていません。|  
|SCC_E_ALREADYCHECKEDOUT|ユーザーは既にファイルをチェックアウトしています。|  
|SCC_E_FILEISLOCKED|ファイルがロックされているため、新しいバージョンの作成が禁止されています。|  
|SCC_E_FILEOUTEXCLUSIVE|別のユーザーがこのファイルに対して排他チェックアウトを実行しました。|  
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
