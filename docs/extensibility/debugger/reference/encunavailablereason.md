---
description: エディットコンティニュが使用できない理由を表します。
title: EncUnavailableReason |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e1f80dc1454cb1c15feddd099411bcb339dbc58c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151005"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!`**エディットコンティニュ** が使用できない理由を表します。

## <a name="syntax"></a>構文

```cpp
enum tagEncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
typedef enum tagEncUnavailableReason EncUnavailableReason;
```

```csharp
public enum EncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
```

## <a name="fields"></a>フィールド
`ENCUN_NONE`\
エディットコンティニュを使用できない具体的な理由はありません。

`ENCUN_INTEROP`\
エディットコンティニュは、相互運用呼び出し中には使用できません。

`ENCUN_SQLCLR`\
エディットコンティニュは、共通言語ランタイム (CLR) を使用する SQL プロシージャ呼び出しでは使用できません。

`ENCUN_MINIDUMP`\
ミニダンプの処理中は、エディットコンティニュは使用できません。

`ENCUN_EMBEDDED`\
エディットコンティニュは、埋め込みコードを処理するときには使用できません。

`ENCUN_ATTACH`\
セッションがデバッガーにアタッチされていないため、エディットコンティニュを使用できません。

`ENCUN_WIN64`\
64ビットの Windows コードの処理中は、エディットコンティニュを使用できません。

## <a name="remarks"></a>解説
この列挙体は、によってのみ内部で使用され [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。 カスタムポート供給業者によって実装される [Getencの状態](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) および [disableenc](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) メソッドは、常にを返す必要があり `E_NOTIMPL` ます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg .idl

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
