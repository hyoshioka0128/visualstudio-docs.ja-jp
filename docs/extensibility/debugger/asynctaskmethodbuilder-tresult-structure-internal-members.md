---
description: このトピックでは、AsyncTaskMethodBuilder クラスの内部メンバーについて説明します。
title: AsyncTaskMethodBuilder &lt; TResult &gt; 構造体内部メンバー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 253d4fa79280fbb49ff0292121c0d0a5cfe4bdb2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055519"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>AsyncTaskMethodBuilder &lt; TResult &gt; 構造体の内部メンバー
このトピックでは、クラスの内部メンバーについて説明し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> ます。 このクラスに関する一般的な情報については、リファレンストピックを参照してください <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 。

 **名前空間:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll)

 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>Syntax

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部メンバー

|Name|Description|
|----------|-----------------|
|[ObjectIdForDebugger プロパティ](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|デバッガーに対してこのビルダーを一意に識別するために使用できるオブジェクトを取得します。|
|[m_task フィールド](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|遅延初期化されたビルドタスクを表します。|

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [.NET Framework の並列拡張の内部構造](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
