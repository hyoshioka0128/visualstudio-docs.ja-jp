---
description: このメソッドは、指定された値を表示するために呼び出されます。
title: IDebugCustomViewer::D isplayValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 238bb4f9b453513f2fdcccb628eacdfc9ef4ae2b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173482"
---
# <a name="idebugcustomviewerdisplayvalue"></a>IDebugCustomViewer::DisplayValue
このメソッドは、指定された値を表示するために呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayValue(
   HWND             hwnd,
   DWORD            dwID,
   IUnknown *       pHostServices,
   IDebugProperty3* pDebugProperty);
);
```

```csharp
int DisplayValue(
   IntPtr          hwnd,
   uint            dwID,
   object          pHostServices,
   IDebugProperty3 pDebugProperty
);
```

## <a name="parameters"></a>パラメーター
`hwnd`\
から親ウィンドウ

`dwID`\
から複数の種類をサポートするカスタムビューアーの ID。

`pHostServices`\
[in] 予約されています。 常に null に設定します。

`pDebugProperty`\
から表示される値を取得するために使用できるインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。

## <a name="remarks"></a>解説
 表示は "モーダル" であり、このメソッドは必要なウィンドウを作成し、値を表示し、入力を待機し、ウィンドウを閉じてから呼び出し元に戻るようにします。 つまり、メソッドは、出力用のウィンドウの作成から、ユーザー入力を待ってウィンドウを破棄するなど、プロパティの値を表示するすべての側面を処理する必要があります。

 指定された [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) オブジェクトの値の変更をサポートするために、値を文字列として表現できる場合は、 [Setvalueasstringwitherror](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) メソッドを使用できます。 それ以外の場合は、 `DisplayValue` インターフェイスを実装するのと同じオブジェクト上で、このメソッドを実装する式エバリュエーターに限定したカスタムインターフェイスを作成する必要があり `IDebugProperty3` ます。 このカスタムインターフェイスには、任意のサイズまたは複雑さのデータを変更するためのメソッドが用意されています。

## <a name="see-also"></a>関連項目
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
