---
title: SccUninitialize 解除関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bcb0b3a6718cc90db6f7176c823ccccbbfc05f9a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190850"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ソース管理プラグインをシャットダウンする準備として、 [Sccinitialize](../extensibility/sccinitialize-function.md) の前回の呼び出しで作成された割り当てまたは開いている接続をクリーンアップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccUninitialize (  
   LPVOID pvContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pvContext  
 から [Sccinitialize](../extensibility/sccinitialize-function.md)で作成されたソース管理プラグインコンテキスト構造へのポインター。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|クリーンアップが正常に完了しました。|  
  
## <a name="remarks"></a>注釈  
 ソース管理プラグインは、シャットダウンの準備を行い、プラグインによってコンテキスト構造に割り当てられたメモリを解放します。 関数は、プラグインの特定のインスタンスごとに1回呼び出されます。 [Sccinitialize](../extensibility/sccinitialize-function.md)の呼び出しは、この呼び出しの前になります。 を呼び出した時点でまだ開いているプロジェクトはありません `SccUninitialize` 。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)
