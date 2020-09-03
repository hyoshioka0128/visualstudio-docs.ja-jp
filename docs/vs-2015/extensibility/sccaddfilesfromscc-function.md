---
title: SccAddFilesFromSCC 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d5af748c9180644cae928d1b6db3a3f880b6b286
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200906"
---
# <a name="sccaddfilesfromscc-function"></a>SccAddFilesFromSCC 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ソース管理から現在開いているプロジェクトにファイルの一覧を追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
SCCRTN SccAddFilesFromSCC(  
   LPVOID  pContext,  
   HWND    hWnd,  
   LPSTR   lpUser,  
   LPSTR   lpAuxProjPath,  
   LONG    cFiles,  
   LPCSTR* lpFilePaths,  
   LPCSTR  lpDestination,  
   LPCSTR  lpComment,  
   LPBOOL  pbResults  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pContext  
 からソース管理プラグインのコンテキストポインター。  
  
 hWnd  
 からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。  
  
 lpUser  
 [入力、出力]ユーザー名 (null 終端文字を含む SCC_USER_SIZE まで)。  
  
 lpAuxProjPath  
 [入力、出力]プロジェクトを識別する補助文字列 ( `SCC_PRJPATH_` null 終端文字を含む、最大サイズまで)。  
  
 cFiles  
 からによって指定されたファイルの数 `lpFilePaths` 。  
  
 lpFilePaths  
 [入力、出力]現在のプロジェクトに追加するファイル名の配列。  
  
 lpDestination  
 からファイルの書き込み先のパス。  
  
 lpComment  
 から追加する各ファイルに適用されるコメント。  
  
 pbResults  
 [入力、出力]各ファイルに対して成功 (0 以外または TRUE) または失敗 (0 または FALSE) を示すフラグの配列 (配列のサイズは、少なくとも long である必要があり `cFiles` ます)。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_E_PROJNOTOPEN|プロジェクトが開いていません。|  
|SCC_E_OPNOTPERFORMED|接続は、によって指定されたプロジェクトと同じではありません `lpAuxProjPath.`|  
|SCC_E_NOTAUTHORIZED|ユーザーには、データベースを更新する権限がありません。|  
|SCC_E_NONSPECIFICERROR|不明なエラー。|  
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
