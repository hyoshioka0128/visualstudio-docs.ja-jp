---
title: Iデバッグエンジン2::ゲットエンジンID |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::GetEngineID
helpviewer_keywords:
- IDebugEngine2::GetEngineID
ms.assetid: 0d5674c8-a9b9-4b72-8211-d2d68695775a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f4071e8279c2c4ab615ff625c1bbedebfd8e64ad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731080"
---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
デバッグ エンジン (DE) の GUID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEngineID(
    GUID* pguidEngine
);
```

```csharp
int GetEngineID(
    out Guid pguidEngine
);
```

## <a name="parameters"></a>パラメーター
`pguidEngine`\
[アウト]DE の GUID を返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
一般的な GUID の例`guidScriptEng`として`guidNativeEng`は、 `guidSQLEng`、または が挙げるものがあります。 新しいデバッグ エンジンは、識別用に独自の GUID を作成します。

## <a name="example"></a>例
`CEngine` [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を次の例に示します。

```cpp
HRESULT CEngine::GetEngineId(GUID *pguidEngine) {
    if (pguidEngine) {
        // Set pguidEngine to guidBatEng, as defined in the Batdbg.idl file.
        // Other languages would require their own guidDifferentEngine to be
        //defined in the Batdbg.idl file.
        *pguidEngine = guidBatEng;
        return NOERROR; // This is typically S_OK.
    } else {
        return E_INVALIDARG;
    }
}
```

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
