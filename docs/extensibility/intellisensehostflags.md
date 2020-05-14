---
title: インテッリセンスホストフラグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IntellisenseHostFlags
helpviewer_keywords:
- IntelliSense, IntellisenseHostFlags enumeration
- IntellisenseHostFlags enumeration
ms.assetid: 0930640b-eb84-48ef-a8f7-d4268f55c99c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a0df05e7363db01bd4f16fee5d75141dc93df1c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710269"
---
# <a name="intellisensehostflags"></a>IntelliSenseHostFlags
IntelliSense ホスト フラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum IntellisenseHostFlags
{
    IHF_READONLYCONTEXT      = 0x00000001
    IHF_NOSEPARATESUBJECT    = 0x00000002
    IHF_SINGLELINESUBJECT    = 0x00000004
    IHF_FORCECOMMITTOCONTEXT = 0x00000008
    IHF_OVERTYPE             = 0x00000010
};
```

### <a name="parameters"></a>パラメーター

|メンバー|説明|
|-------------|-----------------|
|`IHF_READONLYCONTEXT`|コンテキスト バッファーは読み取り専用です。|
|`IHF_NOSEPARATESUBJECT`|件名テキストがありません。 コンテキスト バッファーには、IntelliSense ターゲットが`!IHF_READONLYCONTEXT`含まれています (暗黙的)。|
|`IHF_SINGLELINESUBJECT`|件名テキストは複数行対応ではありません。|
|`IHF_FORCECOMMITTOCONTEXT`|`CanCommitIntoReadOnlyBuffer` と同じ。|
|`IHF_OVERTYPE`|(件名またはコンテキストでの) 編集は、上のタイプ モードで行う必要があります。|

## <a name="requirements"></a>必要条件
 シングルファイルエディタ.idl

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.TextManager.Interop>
