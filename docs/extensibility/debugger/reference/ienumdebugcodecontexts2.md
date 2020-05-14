---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6917c44bb3ddc80513e7c45a6aa4ea0207fd46c9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717270"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
このインターフェイスは、デバッグ セッション、または特定のプログラムまたはドキュメントに関連付けられているコード コンテキストを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugCodeContexts2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、プログラム内の特定のテキストの位置のコード コンテキストの一覧、または特定のドキュメント コンテキストのコード コンテキストの一覧を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 プログラムのソース ドキュメント内の特定のテキスト位置のコード コンテキストの一覧を表すこのインターフェイスを取得するには[、EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)を呼び出します。

 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)を呼び出して、特定のソース ドキュメント内のすべてのコード コンテキストの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugCodeContexts2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|列挙体シーケンス内の指定した数のコード コンテキストを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|列挙シーケンス内の指定した数のコード コンテキストをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|列挙子のコード コンテキストの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio は[EnumCodeContext を](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)呼び出して、次のステートメントを設定するとき、またはソース ファイルの逆アセンブリを表示するときに、ユーザーが選択できるコード コンテキストの一覧を作成します。 複数のコード コンテキストが発生する可能性があります(たとえば、C++ スタイル テンプレートのインスタンスが複数ある場合)。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)
