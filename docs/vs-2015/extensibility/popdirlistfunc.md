---
title: POPDIRLISTFUNC |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 77e4701d3d8ec54fd37d6483f55b10a28af65b15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194054"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

これは、 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 関数に与えられたコールバック関数であり、ディレクトリのコレクションと (必要に応じて) ファイル名を更新して、ソース管理下にある場所を検索します。  
  
 `POPDIRLISTFUNC`コールバックは、実際にソース管理下にあるディレクトリとファイル名 (関数に指定されたリスト内) に対してのみ呼び出す必要があり `SccPopulateDirList` ます。  
  
## <a name="signature"></a>署名  
  
```cpp#  
typedef BOOL (*POPDIRLISTFUNC)(  
   LPVOID pvCallerData,  
   BOOL bFolder,  
   LPCSTR lpDirectoryOrFileName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pvCallerData  
 から [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)に指定されたユーザー値。  
  
 bFolder  
 [入力] `TRUE` 内の名前がディレクトリである場合は `lpDirectoryOrFileName` 。それ以外の場合はファイル名。  
  
 lpDirectoryOrFileName  
 からソースコード管理下にあるディレクトリまたはファイル名への完全なローカルパス。  
  
## <a name="return-value"></a>戻り値  
 IDE から適切なエラーコードが返されます。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|処理し続けます。|  
|SCC_I_OPERATIONCANCELED|処理を停止します。|  
|SCC_E_xxx|適切なソース管理エラーが発生すると、処理が停止します。|  
  
## <a name="remarks"></a>注釈  
 関数のパラメーターにフラグが含まれている場合、 `fOptions` `SccPopulateDirList` `SCC_PDL_INCLUDEFILES` リストにはファイル名とディレクトリ名が含まれている可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)   
 [エラー コード](../extensibility/error-codes.md)
