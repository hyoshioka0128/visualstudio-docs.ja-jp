---
title: IDebugSymbolProviderDirect |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect interface
ms.assetid: 872b04a8-70de-4ab5-aceb-684c81828545
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1ad768419786f78277b791997538785265a24c0f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153096"
---
# <a name="idebugsymbolproviderdirect"></a>IDebugSymbolProviderDirect
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

メタデータおよびコアシンボルインターフェイスに直接アクセスできるシンボルプロバイダーを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugSymbolProviderDirect: IUnknown  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetAppIDFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getappidfromaddress.md)|デバッグアドレスに指定されたアプリケーションドメイン識別子を取得します。|  
|[GetCurrentModulesInfo](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesinfo.md)|シンボルグループ内のモジュールに関する情報を取得します。|  
|[GetCurrentModulesState](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesstate.md)|シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。|  
|[GetMetaDataImport](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmetadataimport.md)|メタデータのインポート情報を取得します。|  
|[GetMethodFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmethodfromaddress.md)|指定されたデバッグアドレスのメソッドに関する情報を取得します。|  
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getsymunmanagedreader.md)|アンマネージコードのシンボルリーダーを取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、他のほとんどのシンボルプロバイダーインターフェイスの代わりに使用できます。 メタデータとインターフェイスへの直接アクセスを提供し `CorSym` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
