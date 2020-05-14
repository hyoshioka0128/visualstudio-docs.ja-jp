---
title: DISASSEMBLY_STREAM_SCOPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fae1f22c6db22cd6cff93cfb1b98a28620a1537c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737275"
---
# <a name="disassembly_stream_scope"></a>DISASSEMBLY_STREAM_SCOPE
逆アセンブリ ストリームのスコープを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
typedef DWORD DISASSEMBLY_STREAM_SCOPE;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
```

## <a name="fields"></a>フィールド
`DSS_HUGE`\
コード コンテキストを逆アセンブルすると、クライアントが通常 1 回の呼び出しで取得するよりも多くの出力が生成されることを指定します。

`DSS_FUNCTION`\
コード コンテキストに含まれる関数を逆アセンブルすることを指定します。 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)メソッドによって返される場合、逆アセンブリ ストリームが関数を表すことを指定します。

`DSS_MODULE`\
`IDebugDisassemblyStream2::GetScope`メソッドによって返された場合、逆アセンブリ ストリームがモジュールを表すことを指定します。

`DSS_ALL`\
アドレス 空間全体の逆アセンブリを指定します。

## <a name="remarks"></a>Remarks
メソッドに引数として渡され[、GetScope](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)メソッドによって返されます。 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
