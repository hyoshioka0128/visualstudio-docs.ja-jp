---
title: COMPUTER_INFO |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
スイート マスクを識別します。

`dwOperatingSystemVersion`\
オペレーティング システムのバージョン番号。

## <a name="remarks"></a>Remarks
この構造体は[、GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [コンピュータ情報を取得します。](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)
