---
title: BP_FLAGS90 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5628af4a6e5c4deae3de02340e882bd2605e22d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738050"
---
# <a name="bp_flags90"></a>BP_FLAGS90
オプション フラグの有効な値を列挙します。 オプションのフラグを使用して、ブレークポイントを設定するときに追加情報を指定できます。 この列挙体は[、BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)列挙体を拡張します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE               = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION    = 0x0001,
    BP90_FLAG_DONT_STOP          = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
typedef DWORD BP_FLAGS90;
```

```csharp
public enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE                = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION     = 0x0001,
    BP90_FLAG_DONT_STOP           = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
```

## <a name="fields"></a>フィールド
`BP90_FLAG_NONE`\
ブレークポイント フラグを指定しません。

`BP90_FLAG_MAP_DOCPOSITION`\
デバッグ エンジン (DE) ドキュメントの位置を使用してブレークポイントをマップする必要があることを指定します。 これは、スクリプト指向のソース ファイル (アクティブ サーバー ページ (ASP) など) に設定されたブレークポイントにのみ適用されます。

`BP90_FLAG_DONT_STOP`\
ブレークポイントをデバッグ エンジンで処理する必要がありますが、デバッグ エンジンは最終的にそこで停止しないように指定します。つまり、[イベント](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)オブジェクトを送信できません。 このフラグは、主にトレース・ポイントで使用するように設計されています。

`BP90_FLAG_TRACEPOINT_CONTINUE`\
ステップ実行状態をクリアするかどうかを判断するために、ネイティブデバッグ エンジンによって使用されます。 トレース ポイントがマクロを実行する場合、BP90_FLAG_DONT_STOP設定されないため、BP90_FLAG_DONT_STOPとは異なります。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg90.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
