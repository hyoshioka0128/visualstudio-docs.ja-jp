---
title: 無効な理由 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28863549ab3eac96322530bc85c52697f20448c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737161"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!`エディット**コンティニュ**が使用できない理由を表します。

## <a name="syntax"></a>構文

```cpp
enum tagEncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
typedef enum tagEncUnavailableReason EncUnavailableReason;
```

```csharp
public enum EncUnavailableReason {
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
エディット コンティニュが利用できない理由は特定されていません。

`ENCUN_INTEROP`\
編集と続行は、InterOp 呼び出し中は使用できません。

`ENCUN_SQLCLR`\
エディット コンティニュは、共通言語ランタイム (CLR) を使用する SQL プロシージャ呼び出し中は使用できません。

`ENCUN_MINIDUMP`\
ミニダンプの処理中はエディット コンティニュは使用できません。

`ENCUN_EMBEDDED`\
エディット コンティニュは、埋め込みコードを処理するときには使用できません。

`ENCUN_ATTACH`\
セッションがデバッガにアタッチされ、起動されなかったため、エディット コンティニュは使用できません。

`ENCUN_WIN64`\
エディット コンティニュは、64 ビット Windows コードの処理中は使用できません。

## <a name="remarks"></a>Remarks
この列挙体は、内部で使用[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]する場合にのみ使用します。 カスタム ポート サプライヤによって実装される[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)メソッドと[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)メソッドは、常にを返す`E_NOTIMPL`必要があります。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.idl

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
