---
title: Iデバッグエンジン2::セットレジストリルート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetRegistryRoot
helpviewer_keywords:
- IDebugEngine2::SetRegistryRoot
ms.assetid: d0d81202-8a4a-4bc3-b297-30a047c5ec60
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: beba304e846126b262c23c0fc8232f79de5fd794
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730875"
---
# <a name="idebugengine2setregistryroot"></a>IDebugEngine2::SetRegistryRoot
デバッグ エンジン (DE) のレジストリ ルートを設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetRegistryRoot( 
   LPCOLESTR pszRegistryRoot
);
```

```csharp
int SetRegistryRoot( 
   string pszRegistryRoot
);
```

## <a name="parameters"></a>パラメーター
`pszRegistryRoot`\
[in]使用するレジストリ ルート。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドでは[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]、DE がレジストリ設定を取得するために使用する代替レジストリ ルートを指定できます。たとえば、"HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\8.0Exp"。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
