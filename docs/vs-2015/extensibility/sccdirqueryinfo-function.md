---
title: SccDirQueryInfo 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7334ddd1ce6c7f9feac63253246e55b65121e18b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841353"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、現在の状態の完全修飾ディレクトリの一覧を調べます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccDirQueryInfo(  
LPVOID  pContext,  
LONG    nDirs,  
LPCSTR* lpDirNames,  
LPLONG  lpStatus  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pContext  
 からソース管理プラグインのコンテキスト構造。  
  
 nDirs  
 からクエリ対象として選択されたディレクトリの数。  
  
 lpDirNames  
 から照会するディレクトリの完全修飾パスの配列。  
  
 lpStatus  
 [入力、出力]ステータスフラグを返すソース管理プラグインの配列構造体。詳細については、「 [ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md) 」を参照してください。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|クエリが正常に実行されました。|  
|SCC_E_OPNOTSUPPORTED|ソースコード管理システムでは、この操作はサポートされていません。|  
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|  
  
## <a name="remarks"></a>注釈  
 関数は、返される配列にファミリのビットのビットマスク `SCC_DIRSTATUS` ( [ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md)を参照) を入力します。これは、指定されたディレクトリごとに1つのエントリです。 状態配列は、呼び出し元によって割り当てられます。  
  
 IDE では、ディレクトリの名前を変更する前に、この関数を使用して、ディレクトリがソース管理下にあるかどうかを、対応するプロジェクトがあるかどうかを照会することによって確認します。 ディレクトリがソース管理下にない場合、IDE はユーザーに適切な警告を提供できます。  
  
> [!NOTE]
> ソース管理プラグインが1つ以上の状態値を実装しないことを選択した場合は、実装されていないビットを0に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [ディレクトリの状態コード](../extensibility/directory-status-code-enumerator.md)
