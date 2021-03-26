---
description: シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。
title: 'IDebugSymbolProviderDirect:: Getcurrentモジュール State |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetCurrentModulesState
- IDebugSymbolProviderDirect::GetCurrentModulesState
ms.assetid: a0c85318-5686-4eed-b213-21f2b9e681e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e5bc7af275d18626fdb86e25400e9433002be8cf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081309"
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

## <a name="remarks"></a>注釈
 モジュールがシンボルグループに追加されるか、シンボルグループから削除されるたびに、状態が変更されます。 そのため、このメソッドを使用して、シンボルグループが変更されているかどうかを検出できます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
