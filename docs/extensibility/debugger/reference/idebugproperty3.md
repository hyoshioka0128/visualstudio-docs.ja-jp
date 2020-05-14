---
title: Iデバッグプロパティ3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3
helpviewer_keywords:
- IDebugProperty3 interface
ms.assetid: 8f9be68d-4490-4eca-8f6b-8a10ed77e226
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d2819724c204631112fd1a3e827126c4bc176972
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721046"
---
# <a name="idebugproperty3"></a>IDebugProperty3
このインターフェイスは、次の機能をサポートします。

- プロパティに関連付けられた任意の長い文字列を取得します。

- 一意の ID をプロパティに関連付けます。

- プロパティのカスタム ビューアーの一覧を取得しています。

- 結果のエラーを報告する機能を持つプロパティの値を設定する

## <a name="syntax"></a>構文

```
IDebugProperty3 : IDebugProperty2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、長い文字列、プロパティ ID、およびカスタム ビューアーのサポートを提供する[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugProperty2`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 から`IDebugProperty2`継承されたメソッドに加えて、インターフェイス`IDebugProperty3`は、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)|プロパティに関連付けられた文字列の長さを返します。|
|[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)|ユーザーが指定したバッファー内の文字列を返します。|
|[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)|このプロパティの一意の ID を作成します。|
|[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)|このプロパティの一意の ID を破棄します。|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)|このプロパティを表示できるカスタム ビューアーの数を返します。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)|このプロパティを表示できるカスタム ビューアーの一覧を返します。|
|[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)|このプロパティの値を設定し、問題が発生した場合はエラー メッセージを返します。|

## <a name="remarks"></a>Remarks
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)セッション デバッグ マネージャー (SDM) がプロパティの値を設定する場合は、このメソッドを使用することをお勧めします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
