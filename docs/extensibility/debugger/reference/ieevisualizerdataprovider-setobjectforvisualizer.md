---
title: 'IEEVisualizerDataProvider:: SetObjectForVisualizer |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer method
ms.assetid: 40dad2be-57ff-4f74-9d82-c48039c125c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab63f1e74e0cd3ac64a4d7e7687a9136075b41a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718081"
---
# <a name="ieevisualizerdataprovidersetobjectforvisualizer"></a>IEEVisualizerDataProvider::SetObjectForVisualizer
このメソッドは、ビジュアライザーが表すオブジェクトを変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetObjectForVisualizer(
   IDebugObject*  pNewObject,
   BSTR*          error,
   IDebugObject** pException
);
```

```csharp
int SetObjectForVisualizer(
   IDebugObject     pNewObject,
   out string       error,
   out IDebugObject pException
);
```

## <a name="parameters"></a>パラメーター
`pNewObject`\
から設定するオブジェクト。

`error`\
入出力オブジェクトの設定中にエラーが発生した場合、この文字列にはエラーメッセージが格納されます。

`pException`\
入出力エラーが発生した場合、このオブジェクトは例外情報を保持します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 エラー情報が返される方法は、実装者が決定します。 ただし、一部の呼び出し元では、エラーが発生したことを認識するために例外オブジェクトが返されたかどうかのみを調べることができます。したがって、エラーが発生した場合、このメソッドは常に例外オブジェクトを返します。 エラー文字列は、呼び出し元が使用しようとしている場合にも指定する必要があります。

## <a name="see-also"></a>関連項目
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
