---
description: 指定したプロパティまたはフィールドに表示する値文字列の数を取得します。
title: 'IEEVisualizerService:: GetValueDisplayStringCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IEEVisualizerService::GetValueDisplayStringCount
- GetValueDisplayStringCount
ms.assetid: d683a833-fbfb-4042-84df-6905124a268a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b77e2537e7581bb15f6458b4515d407fcfa1f827
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222849"
---
# <a name="ieevisualizerservicegetvaluedisplaystringcount"></a>IEEVisualizerService::GetValueDisplayStringCount
指定したプロパティまたはフィールドに表示する値文字列の数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetValueDisplayStringCount (
   DWORD         displayKind,
   IDebugField * propertyOrField,
   ULONG *       pcelt
);
```

```csharp
int GetValueDisplayStringCount (
   uint        displayKind,
   IDebugField propertyOrField,
   out ulong   pcelt
);
```

## <a name="parameters"></a>パラメーター
`displayKind`\
から [Displaykind](../../../extensibility/debugger/reference/displaykind.md) 列挙子の値。

`propertyOrField`\
からプロパティまたはフィールドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイス。

`pcelt`\
入出力表示する値文字列の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
