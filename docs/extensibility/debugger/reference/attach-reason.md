---
description: デバッグエンジン (DE) がプログラムノードにアタッチされる理由を指定します。
title: ATTACH_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f6fa83fb537f05a2c073e3693dab964fa58af464
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144612"
---
# <a name="attach_reason"></a>ATTACH_REASON
デバッグエンジン (DE) がプログラムノードにアタッチされる理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
typedef DWORD ATTACH_REASON;
```

```csharp
public enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
```

## <a name="fields"></a>フィールド
`ATTACH_REASON_AUTO`\
プロセスは現在デバッグモードであるため、アタッチします。

`ATTACH_REASON_LAUNCH`\
プロセスが起動されたため、アタッチします。

`ATTACH_REASON_USER`\
ユーザー要求のためにアタッチします。

## <a name="remarks"></a>解説
これらの値は、 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドと [attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md) メソッドのパラメーターとして使用されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
