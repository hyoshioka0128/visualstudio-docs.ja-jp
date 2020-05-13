---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0aa67792ced94afd9c4439cbc6ea577e6b85f28b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716614"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
このインターフェイスは[、FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugFrameInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、現在の呼び出し履歴を記述する構造体の一覧を提供するには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デバッグ中のプログラムでブレークポイント、例外、または停止が発生するたびに、このインターフェイスを取得する[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugFrameInfo2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|列挙体シーケンス内の指定した数の[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体を取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|列挙体シーケンス内の指定した数の[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|列挙子内の[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体の数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio は、デバッグ中のプログラムでブレークポイント、例外、またはユーザーが生成した一時停止を処理する最初の手順として、このインターフェイスを取得します。 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体のリストは、現在の呼び出し履歴を表し、現在の関数呼び出しはリストの先頭に、最も古い関数呼び出しはリストの末尾にあります。 それぞれが`FRAMEINFO`スタックフレームを表し、式を評価し、ローカル変数を参照するコンテキストを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
