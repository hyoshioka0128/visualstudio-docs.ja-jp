---
title: プロパティ 3::カスタム ビューアーリスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerList
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerList
ms.assetid: 74490fd8-6f44-4618-beea-dab64961bb8a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 212f8d251232d35ee7d9cc46074a21239eea29f4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721165"
---
# <a name="idebugproperty3getcustomviewerlist"></a>IDebugProperty3::GetCustomViewerList
このプロパティに関連付けられているカスタム ビューアーのリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomViewerList(
    ULONG                celtSkip,
    ULONG                celtRequested,
    DEBUG_CUSTOM_VIEWER* rgViewers,
    ULONG*               pceltFetched
);
```

```csharp
int GetCustomViewerList(
    uint                  celtSkip,
    uint                  celtRequested,
    DEBUG_CUSTOM_VIEWER[] rgViewers,
    out uint              pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celtSkip`\
[in]スキップするビューアーの数。

`celtRequested`\
[in]取得するビューアーの数 (`rgViewers`配列のサイズも指定)。

`rgViewers`\
[イン、アウト]入力する[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)構造体の配列。

`pceltFetched`\
[アウト]実際に返されたビューアーの数。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
型ビジュアライザーをサポートするには、このメソッドは呼び出しを[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)メソッドに転送します。 式エバリュエーターがこのプロパティの型のカスタム ビューアーもサポートしている場合、このメソッドは、適切なカスタム ビューアーを一覧に追加できます。

[型ビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)の違いについては、「型ビジュアライザー」と「カスタム ビューアー」を参照してください。

## <a name="example"></a>例
次の例は[、IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを公開する**CProperty**オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP CProperty::GetCustomViewerList(ULONG celtSkip, ULONG celtRequested, DEBUG_CUSTOM_VIEWER* prgViewers, ULONG* pceltFetched)
{
    if (NULL == prgViewers)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerList(celtSkip, celtRequested, prgViewers, pceltFetched);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
