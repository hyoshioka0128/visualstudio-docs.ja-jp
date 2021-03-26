---
description: この記事では、AsyncTaskMethodBuilder クラスの内部メンバーについて説明します。
title: AsyncTaskMethodBuilder 構造体の内部メンバー
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncTaskMethodBuilder structure [.NET Framework]
- AsyncTaskMethodBuilder structure [.NET Framework debug engines]
ms.assetid: f32f5857-7ef8-45fd-8b5a-7f644eb98b11
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f76d6156928f983a3eb93e7a33b50ff46ec9e87d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055532"
---
# <a name="asynctaskmethodbuilder-structure---internal-members"></a>AsyncTaskMethodBuilder 構造体の内部メンバー
このトピックでは、クラスの内部メンバーについて説明し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> ます。 このクラスに関する一般的な情報については、リファレンストピックを参照してください <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 。

 **名前空間:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll)

 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>Syntax

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部メンバー

|Name|Description|
|----------|-----------------|
|[ObjectIdForDebugger プロパティ](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|デバッガーに対してこのビルダーを一意に識別するために使用できるオブジェクトを取得します。|
|[m_builder フィールド](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|この非ジェネリックインスタンスがデリゲートするジェネリックビルダーオブジェクトを表します。|

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>
- [.NET Framework の並列拡張の内部構造](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
