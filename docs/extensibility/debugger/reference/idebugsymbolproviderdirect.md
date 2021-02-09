---
title: IDebugSymbolProviderDirect |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect interface
ms.assetid: 872b04a8-70de-4ab5-aceb-684c81828545
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29f0e7e3d2fefe0f47dc971ebff273bf2745a5ef
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909426"
---
# <a name="idebugsymbolproviderdirect"></a>IDebugSymbolProviderDirect
メタデータおよびコアシンボルインターフェイスに直接アクセスできるシンボルプロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugSymbolProviderDirect: IUnknown
```

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetAppIDFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getappidfromaddress.md)|デバッグアドレスに指定されたアプリケーションドメイン識別子を取得します。|
|[GetCurrentModulesInfo](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesinfo.md)|シンボルグループ内のモジュールに関する情報を取得します。|
|[GetCurrentModulesState](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesstate.md)|シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。|
|[GetMetaDataImport](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmetadataimport.md)|メタデータのインポート情報を取得します。|
|[GetMethodFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmethodfromaddress.md)|指定されたデバッグアドレスのメソッドに関する情報を取得します。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getsymunmanagedreader.md)|アンマネージコードのシンボルリーダーを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、他のほとんどのシンボルプロバイダーインターフェイスの代わりに使用できます。 メタデータとインターフェイスへの直接アクセスを提供し `CorSym` ます。

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
