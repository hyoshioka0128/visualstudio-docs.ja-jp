---
title: データプロバイダー::セットオブジェクトフォービジュアライザー |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
[in]設定するオブジェクト。

`error`\
[アウト]オブジェクトの設定時にエラーが発生した場合、この文字列にはエラー メッセージが表示されます。

`pException`\
[アウト]エラーが発生した場合、このオブジェクトは例外情報を保持します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 エラー情報の返し方は、実装者の判断に応じます。 ただし、エラーが発生したことを知るために例外オブジェクトが返されたかどうかを確認するだけの呼び出し元が存在する場合があるため、エラーが発生した場合、このメソッドは常に例外オブジェクトを返す必要があります。 呼び出し元がエラー文字列を使用する場合にも、エラー文字列を指定する必要があります。

## <a name="see-also"></a>関連項目
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
