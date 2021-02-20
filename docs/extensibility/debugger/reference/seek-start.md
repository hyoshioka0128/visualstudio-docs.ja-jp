---
title: SEEK_START |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SEEK_START
helpviewer_keywords:
- SEEK_START enumeration
ms.assetid: 55bd8901-626e-428b-a263-23b14417f4c6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 833a1e1b18e28070d50882fcfb485d0b6797ad20
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965487"
---
# <a name="seek_start"></a>SEEK_START
逆アセンブリストリームでシークを開始する位置を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_SEEK_START { 
   SEEK_START_BEGIN       = 0x0001,
   SEEK_START_END         = 0x0002,
   SEEK_START_CURRENT     = 0x0003,
   SEEK_START_CODECONTEXT = 0x0004,
   SEEK_START_CODELOCID   = 0x0005
};
typedef DWORD SEEK_START;
```

```csharp
public enum enum_SEEK_START { 
   SEEK_START_BEGIN       = 0x0001,
   SEEK_START_END         = 0x0002,
   SEEK_START_CURRENT     = 0x0003,
   SEEK_START_CODECONTEXT = 0x0004,
   SEEK_START_CODELOCID   = 0x0005
};
```

## <a name="fields"></a>フィールド
 `SEEK_START_BEGIN`\
 現在のドキュメントの先頭からシークを開始します。

 `SEEK_START_END`\
 現在のドキュメントの末尾からシークを開始します。

 `SEEK_START_CURRENT`\
 現在のドキュメントの現在位置からシークを開始します。

 `SEEK_START_CODECONTEXT`\
 現在のドキュメントの指定されたコードコンテキストでシークを開始します。

 `SEEK_START_CODELOCID`\
 指定されたコード位置識別子でシークを開始します。 コードの場所の識別子は、 [Getcurrentlocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)を呼び出すことによって取得されます。

## <a name="remarks"></a>解説
 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)メソッドに引数として渡されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
