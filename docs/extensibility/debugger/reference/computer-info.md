---
title: COMPUTER_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- COMPUTER_INFO structure
ms.assetid: 943085b2-f165-462d-9a4e-2086f0cdfff4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27794dff51646b72dbbfda81ead02e5206ade78b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737662"
---
# <a name="computer_info"></a>COMPUTER_INFO
デバッガーが実行されているコンピューターについて説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagCOMPUTER_INFO
{
    WORD wProcessorArchitecture;
    WORD wSuiteMask;
    DWORD dwOperatingSystemVersion;
} COMPUTER_INFO;
```

```csharp
public struct COMPUTER_INFO
{
    public ushort wProcessorArchitecture;
    public ushort wSuiteMask;
    public uint dwOperatingSystemVersion;
}
```

## <a name="members"></a>メンバー
`wProcessorArchitecture`\
マイクロプロセッサのアーキテクチャを識別します。

`wSuiteMask`\
Suite マスクを識別します。

`dwOperatingSystemVersion`\
オペレーティングシステムのバージョン番号。

## <a name="remarks"></a>解説
この構造体は、 [Getcomputerinfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md) メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)
