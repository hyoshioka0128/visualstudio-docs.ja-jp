---
title: BP_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_FLAGS
helpviewer_keywords:
- BP_FLAGS enumeration
ms.assetid: c45dfc74-5e7f-4f1e-a147-ab2a55dccbd0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62626ff75a4545d89835d3136649191004291f8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738061"
---
# <a name="bp_flags"></a>BP_FLAGS
ブレークポイントを設定するときに追加情報を指定するために使用できるオプションのフラグを提供します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
typedef DWORD BP_FLAGS;
```

```csharp
public enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
```

## <a name="fields"></a>フィールド
`BP_FLAG_NONE`\
ブレークポイント フラグを指定しません。

`BP_FLAG_MAP_DOCPOSITION`\
デバッグ エンジン (DE) がドキュメントの位置を使用してブレークポイントをマップする必要があることを指定します。 これは、スクリプト指向のソース ファイル (アクティブ サーバー ページ (ASP) など) に設定されたブレークポイントにのみ適用されます。

`BP_FLAG_DONT_STOP`\
ブレークポイントはデバッグ エンジンによって処理される必要がありますが、デバッグ エンジンは最終的にそこで停止しないように指定します (つまり[、IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)イベント オブジェクトを送信しないでください)。 このフラグは、主にトレースポイントで使用するように設計されています。

## <a name="remarks"></a>Remarks
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)構造体および`dwFlags`[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体のメンバーに使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
