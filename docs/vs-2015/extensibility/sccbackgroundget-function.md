---
title: SccBackgroundGet 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 118d8458fd9581a87baea08452d0011d4d66c9a1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841612"
---
# <a name="sccbackgroundget-function"></a>SccBackgroundGet 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、指定された各ファイルを、ユーザー操作なしでソース管理から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
SCCRTN SccBackgroundGet(  
   LPVOID  pContext,  
   LONG    nFiles,  
   LPCSTR* lpFileNames,  
   LONG    dwFlags,  
   LONG    dwBackgroundOperationID  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pContext  
 からソース管理プラグインのコンテキストポインター。  
  
 nFiles  
 から配列に指定されたファイルの数 `lpFileNames` 。  
  
 lpFileNames 名  
 [入力、出力]取得するファイルの名前の配列。  
  
> [!NOTE]
> 名前は、完全修飾されたローカルファイル名である必要があります。  
  
 dwFlags  
 からコマンドフラグ ( `SCC_GET_ALL` 、 `SCC_GET_RECURSIVE` )。  
  
 dwBackgroundOperationID  
 からこの操作に関連付けられている一意の値。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|操作は正常に完了しました。|  
|SCC_E_BACKGROUNDGETINPROGRESS|バックグラウンドでの取得が既に進行中である (ソース管理プラグインは、同時バッチ操作をサポートしていない場合にのみ、これを返す必要があります)。|  
|SCC_I_OPERATIONCANCELED|操作が完了する前に取り消されました。|  
  
## <a name="remarks"></a>注釈  
 この関数は、ソース管理プラグインが読み込まれたスレッドとは異なるスレッド上で常に呼び出されます。 この関数は、完了するまでを返すことは想定されていません。ただし、ファイルの複数のリストを使用して複数回呼び出すことができます。  
  
 引数の使用 `dwFlags` は [Sccget](../extensibility/sccget-function.md)と同じです。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccGet](../extensibility/sccget-function.md)
