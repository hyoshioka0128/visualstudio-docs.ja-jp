---
title: IEE ビジュアライザーサービス::カスタム ビューアー リスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerList
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerList method
ms.assetid: 249d26ca-914f-43af-a400-8162477223f4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f3808ad6fb511270ee3825601c476f10a8b77124
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718019"
---
# <a name="ieevisualizerservicegetcustomviewerlist"></a>IEEVisualizerService::GetCustomViewerList
このメソッドは、このサービスが認識しているビジュアライザー型のリストを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomViewerList(
   ULONG                celtSkip,
   ULONG                celtRequested,
   DEBUG_CUSTOM_VIEWER* rgViewers,
   ULONG*               pceltFetched
);
```

```csharp
int GetCustomViewerList(
   uint                  celtSkip,
   uint                  celtRequested,
   DEBUG_CUSTOM_VIEWER[] rgViewers,
   out uint              pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celtSkip`\
[in]スキップするビジュアライザーの数。

`celRequested`\
[in]取得するビジュアライザーの数 (`rgViewers`配列のサイズも指定)。

`rgViewers`\
[イン、アウト]入力する[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)構造体の配列。

`pceltFetched`\
[アウト]実際に取得されたビジュアライザーの数。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
- [型](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)ビジュアライザーのサポートの一環として、このメソッドに要求を渡します。 式エバリュエーターが同じ型のカスタム ビューアーも提供する場合、それらのカスタム ビューアーの適切に入力された[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)構造をリストに追加できます。 これらの追加[ビューアーが](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)反映されていることを確認します。

 [ビジュアライザーとビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)の違いについては、「タイプ ビジュアライザー」と「カスタム ビューアー」をご参照ください。

## <a name="see-also"></a>関連項目
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
