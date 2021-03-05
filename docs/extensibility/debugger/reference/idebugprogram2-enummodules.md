---
description: このプログラムによって読み込まれ、実行されているモジュールの一覧を取得します。
title: 'IDebugProgram2:: EnumModules |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumModules
helpviewer_keywords:
- IDebugProgram2::EnumModules
ms.assetid: 876ac9da-3b7c-4156-b79a-8f340e9fcea6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26016510856de44c07ca9a123553e82d0d2a79f4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149627"
---
# <a name="idebugprogram2enummodules"></a>IDebugProgram2::EnumModules
このプログラムによって読み込まれ、実行されているモジュールの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumModules( 
   IEnumDebugModules2** ppEnum
);
```

```csharp
int EnumModules( 
   out IEnumDebugModules2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力モジュールの一覧を含む [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 モジュールは DLL またはアセンブリであり、通常は **モジュール** デバッグウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
