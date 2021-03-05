---
description: シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。
title: 'IDebugSymbolProviderDirect:: Getcurrentモジュール State |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetCurrentModulesState
- IDebugSymbolProviderDirect::GetCurrentModulesState
ms.assetid: a0c85318-5686-4eed-b213-21f2b9e681e6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fcc127bd3450f06a51ab0b04d61d52f4ee08e092
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149484"
---
# <a name="idebugsymbolproviderdirectgetcurrentmodulesstate"></a>IDebugSymbolProviderDirect::GetCurrentModulesState
シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCurrentModulesState(
    DWORD*          pState,
    unsigned long * count
);
```

```csharp
int GetCurrentModulesState(
    out uint pState,
    out uint count
);
```

## <a name="parameters"></a>パラメーター
`pState`\
入出力シンボルプロバイダーグループの状態。

`count`\
入出力グループ内のモジュールの数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 モジュールがシンボルグループに追加されるか、シンボルグループから削除されるたびに、状態が変更されます。 そのため、このメソッドを使用して、シンボルグループが変更されているかどうかを検出できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
