---
description: このメソッドは、このサービスが認識している型ビジュアライザーのリストを返します。
title: 'IEEVisualizerService:: GetCustomViewerList |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerList
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerList method
ms.assetid: 249d26ca-914f-43af-a400-8162477223f4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 99db28a8d0efef7ffec97ecab818f4ede6b153fe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086886"
---
# <a name="ieevisualizerservicegetcustomviewerlist"></a>IEEVisualizerService::GetCustomViewerList
このメソッドは、このサービスが認識している型ビジュアライザーのリストを返します。

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
からスキップするビジュアライザーの数。

`celRequested`\
から取得するビジュアライザーの数 (配列のサイズも指定し `rgViewers` ます)。

`rgViewers`\
[入力、出力]入力する [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 構造体の配列。

`pceltFetched`\
入出力実際に取得されたビジュアライザーの数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) は、型ビジュアライザーのサポートの一部として、このメソッドに要求を渡します。 式エバリュエーターでも同じ種類のカスタムビューアーが提供される場合、それらのカスタムビューアーに対して適切に入力された [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 構造を一覧に追加できます。 [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)にこれらの追加のビューアーが反映されていることを確認します。

 ビジュアライザーとビューアーの違いの詳細については、「 [型ビジュアライザーとカスタムビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) 」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
