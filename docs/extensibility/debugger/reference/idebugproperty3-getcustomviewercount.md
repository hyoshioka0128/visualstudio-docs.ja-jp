---
description: このプロパティで使用できるカスタムビューアーの数を取得します。
title: 'IDebugProperty3:: GetCustomViewerCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerCount
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerCount
ms.assetid: dc5bb3e4-dc85-46e4-98fa-c6be8583b985
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58ad7ffc1b3250f5002f9f08208c464d14a2cc15
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171397"
---
# <a name="idebugproperty3getcustomviewercount"></a>IDebugProperty3::GetCustomViewerCount
このプロパティで使用できるカスタムビューアーの数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomViewerCount(
    ULONG* pcelt
);
```

```csharp
int GetCustomViewerCount(
    out uint pcelt
);
```

## <a name="parameters"></a>パラメーター
`pcelt`\
入出力このプロパティで使用できるカスタムビューアーの数。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
型ビジュアライザーをサポートするために、このメソッドは呼び出しを [GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) メソッドに転送します。 式エバリュエーターがこのプロパティの型のカスタムビューアーもサポートしている場合、このメソッドは、返された値にカスタムビューアーの数を追加します。

型ビジュアライザーとカスタムビューアーの違いの詳細については、「 [型ビジュアライザーとカスタムビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)」を参照してください。

## <a name="example"></a>例
次の例は、 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを公開する **cproperty** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP CProperty::GetCustomViewerCount(ULONG* pcelt)
{
    if (pcelt == NULL)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerCount(pcelt);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
