---
description: 逆アセンブリストリームのスコープを指定します。
title: DISASSEMBLY_STREAM_SCOPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 828d6b9afc659a09a4f1091c741e6246512de025
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096175"
---
# <a name="disassembly_stream_scope"></a>DISASSEMBLY_STREAM_SCOPE
逆アセンブリストリームのスコープを指定します。

## <a name="syntax"></a>Syntax

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
通常、1回の呼び出しでクライアントが取得するよりも多くの出力を生成するように、コードコンテキストの逆アセンブルを行うように指定します。

`DSS_FUNCTION`\
コードコンテキストに含まれる関数を逆アセンブルする必要があることを指定します。 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)メソッドによって返されるときに、逆アセンブリストリームが関数を表すことを指定します。

`DSS_MODULE`\
メソッドによって返された場合 `IDebugDisassemblyStream2::GetScope` 、逆アセンブリストリームがモジュールを表すことを指定します。

`DSS_ALL`\
アドレス空間全体の逆アセンブリを指定します。

## <a name="remarks"></a>注釈
[Getdisassemblystream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)メソッドに引数として渡され、 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)メソッドによって返されます。

これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
