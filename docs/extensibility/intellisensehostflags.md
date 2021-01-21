---
title: IntelliSenseHostFlags |Microsoft Docs
description: IntelliSenseHostFlags 列挙体は、IntelliSense ホストフラグを指定します。 この記事では、列挙値について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b206cc4aa7c1ff388d6868fa8a0533d15da094ff
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487505"
---
# <a name="intellisensehostflags"></a>IntelliSenseHostFlags
IntelliSense ホストフラグを指定します。

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

|メンバー|Description|
|-------------|-----------------|
|`IHF_READONLYCONTEXT`|コンテキストバッファーは読み取り専用です。|
|`IHF_NOSEPARATESUBJECT`|件名のテキストはありません。 コンテキストバッファーに IntelliSense-target (を意味します) が含まれてい `!IHF_READONLYCONTEXT` ます。|
|`IHF_SINGLELINESUBJECT`|件名のテキストは、複数行に対応していません。|
|`IHF_FORCECOMMITTOCONTEXT`|`CanCommitIntoReadOnlyBuffer` と同じ。|
|`IHF_OVERTYPE`|編集 (件名またはコンテキスト) は、上書きモードで実行する必要があります。|

## <a name="requirements"></a>要件
 SingleFileeditor .idl

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.TextManager.Interop>
