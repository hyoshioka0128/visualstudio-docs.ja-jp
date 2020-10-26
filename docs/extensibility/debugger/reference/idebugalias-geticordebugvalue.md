---
title: 'IDebugAlias:: Ge Ordebugvalue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd01785fee7ce65296bac940fb19819415139d53
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736480"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
このエイリアスに関連付けられている値を表すマネージコードインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetICorDebugValue(
   IUnknown** ppUnk
);
```

```csharp
int GetICorDebugValue(
   out object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`ppUnk`\
[出力] `IUnknown` この別名に関連付けられている値を表すインターフェイス。 このインターフェイスは、インターフェイスに対してクエリを実行でき `ICorDebugValue` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、マネージ値にのみ適用され `ICorDebugValue` ます (は、.NET Framework で使用できるインターフェイスであり、cordebug .idl ファイルの .NET FRAMEWORK SDK で定義されています)。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
