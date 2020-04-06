---
title: 構造体 - 内部メンバー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncVoidMethodBuilder structure [.NET Framework]
- AsyncVoidMethodBuilder structure [.NET Framework debug engines]
ms.assetid: fe2970ab-d4c5-4355-a8e4-772ee0a57178
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 866a53fae7bb2cc5325112b84d992da6f95af246
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739297"
---
# <a name="asyncvoidmethodbuilder-structure---internal-members"></a>構造体 - 内部メンバー
このトピックでは、クラスの内部メンバーについて<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>説明します。 このクラスの一般的な情報については、<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>参照トピックを参照してください。

 **名前空間:**<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 これらの内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncVoidMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部メンバー

|名前|説明|
|----------|-----------------|
|[プロパティ](../../extensibility/debugger/asyncvoidmethodbuilder-objectidfordebugger-property.md)|デバッガーに対してこのビルダーを一意に識別するために使用できるオブジェクトを取得します。|
|[m_objectIdForDebuggerフィールド](../../extensibility/debugger/asyncvoidmethodbuilder-m-objectidfordebugger-field.md)|このビルダーを一意に識別するためにデバッガーによって使用される、怠惰に初期化されたオブジェクトを表します。|

## <a name="see-also"></a>関連項目
- <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>
- [NET フレームワークの並列拡張内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
