---
title: SccEndBatch 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 986056b1f5202c2fb94d27a8792ed3b0fe308944
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200146"
---
# <a name="sccendbatch-function"></a>SccEndBatch 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ソース管理操作のバッチを終了します。 これらのバッチを入れ子にすることはできません。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccEndBatch(void);  
```  
  
#### <a name="parameters"></a>パラメーター  
 [なし] :  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|操作のバッチが正常に終了しました。|  
|SCC_E_UNKNOWNERROR|不特定のエラーです。|  
  
## <a name="remarks"></a>注釈  
 ソース管理バッチは、複数のプロジェクトまたは複数のコンテキストで同じソース管理操作を実行するために使用されます。 バッチ処理を使用すると、バッチ操作中のユーザーエクスペリエンスから冗長なダイアログボックスを排除できます。 [Sccbeginbatch](../extensibility/sccbeginbatch-function.md)と関数は、 `SccEndBatch` 操作の開始と終了を示すペアとして使用されます。 入れ子にすることはできません。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
