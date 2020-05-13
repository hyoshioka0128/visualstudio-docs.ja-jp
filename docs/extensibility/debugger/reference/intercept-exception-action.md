---
title: INTERCEPT_EXCEPTION_ACTION |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- INTERCEPT_EXCEPTION_ACTION
helpviewer_keywords:
- INTERCEPT_EXCEPTION_ACTION enumeration
ms.assetid: e647f1eb-2932-4447-8c78-3b0d706fb972
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cc44a4fc5264566468777749d5732662ba81ed6d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715065"
---
# <a name="intercept_exception_action"></a>INTERCEPT_EXCEPTION_ACTION
例外をインターセプトするときに実行するアクションを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_INTERCEPT_EXCEPTION_ACTION
{
    IEA_INTERCEPT = 0x0001
}
typedef DWORD INTERCEPT_EXCEPTION_ACTION;
```

```csharp
public enum enum_INTERCEPT_EXCEPTION_ACTION
{
    IEA_INTERCEPT = 0x0001
}
```

## <a name="parameters"></a>パラメーター

`IEA_INTERCEPT`\
現在の例外のインターセプトを有効にします。 これは現在サポートされている唯一の値であり、指定する必要があります。

## <a name="remarks"></a>Remarks
これらの値は[、メソッド](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)に渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
