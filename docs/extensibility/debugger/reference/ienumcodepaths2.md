---
title: をクリックして実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89c8cac9a7c2baa020002fe852330639d7081982
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717717"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
このインターフェイスは、コード パスの一覧を表します。

## <a name="syntax"></a>構文

```
IEnumCodePaths2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、コード パスの一覧を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するには[、列挙型コードパス](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumCodePaths2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|列挙体シーケンス内の指定した数のコード パスを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|列挙体シーケンス内の指定した数のコード パスをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|列挙子のコード パスの数を取得します。|

## <a name="remarks"></a>Remarks
 コード パスは、プログラム内の分岐点または関数呼び出しを表します。 コード パスのリストは、コードの実行に使用されたパスを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
