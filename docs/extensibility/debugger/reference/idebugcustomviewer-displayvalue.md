---
title: カスタムビューアー::Dアイプレイバリュー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32e444d0d6a30484f708d3001b95e7a71856edd5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732442"
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
[in]親ウィンドウ

`dwID`\
[in]複数の種類をサポートするカスタム ビューアーの ID。

`pHostServices`\
[in] 予約されています。 常に null に設定されます。

`pDebugProperty`\
[in]表示する値を取得するために使用できるインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、必要なウィンドウを作成し、値を表示し、入力を待機し、ウィンドウを閉じる前に、呼び出し元に戻る前に、表示は "モーダル" です。 つまり、出力用のウィンドウの作成からユーザー入力の待機、ウィンドウの破棄まで、プロパティの値を表示する方法をすべて処理する必要があります。

 指定された[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)オブジェクトの値の変更をサポートするには、値を文字列として表現できる場合は[、SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)メソッドを使用できます。 それ以外の場合は、カスタム インターフェイスを作成する必要があります ( この`DisplayValue`メソッドを実装する式エバリュエーターに`IDebugProperty3`限定されます ) 、インターフェイスを実装するオブジェクトと同じオブジェクトに対して行います。 このカスタム インターフェイスは、任意のサイズまたは複雑さのデータを変更するためのメソッドを提供します。

## <a name="see-also"></a>関連項目
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
