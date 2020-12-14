---
title: マネージド オブジェクトのカスタム ビューの作成 | Microsoft Docs
description: Visual Studio デバッガーにより、変数ウィンドウにデータが表示されます。 カスタム型を含むデータ型の表示方法をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/08/2019
ms.topic: conceptual
f1_keywords:
- vs.debug.data.elements
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data types, custom
- custom data types
- managed code, custom data types
- autoexp.dat file
- mcee_cs.dat file
- debugger, expanding data types
- mcee_mc.dat file
ms.assetid: 9969e9b2-9008-4729-8a14-0d6deaa61576
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c2248a361837f664b0f78acfe61f6d7588f5258b
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560214"
---
# <a name="create-custom-views-of-managed-objects-c-visual-basic-f-ccli"></a>マネージド オブジェクトのカスタム ビューの作成 (C#、Visual Basic、F#、C++/CLI)
Visual Studio でデバッガーの変数ウィンドウにデータ型を表示する方法をカスタマイズできます。

## <a name="attributes"></a>属性

C#、Visual Basic、F#、および C++ (C++/CLI コードのみ) では、<xref:System.Diagnostics.DebuggerTypeProxyAttribute>、<xref:System.Diagnostics.DebuggerDisplayAttribute>、および <xref:System.Diagnostics.DebuggerBrowsableAttribute> を使用して、カスタム データの展開を追加できます。

.NET Framework 2.0 コードでは、Visual Basic は DebuggerBrowsable 属性をサポートしません。 この制限は、.NET の新しいバージョンで解除されています。

## <a name="visualizers"></a>ビジュアライザー

マネージド データ型を表示するには、ビジュアライザーを記述します。 詳細については、[ビジュアライザーを記述する](create-custom-visualizers-of-data.md)

> [!NOTE]
> C++ コードでは、[デバッガーでの C++ オブジェクトのカスタム ビューの作成](create-custom-views-of-native-objects.md)に関するページで説明されているように、Natvis フレームワークを使用してカスタム データ型の展開を追加できます。

## <a name="see-also"></a>関連項目

- [DebuggerDisplay 属性を使用して、デバッガーに何を表示するかを通知する](../debugger/using-the-debuggerdisplay-attribute.md)
- [DebuggerTypeProxy 属性を使用して、デバッガーにどの型を表示するかを通知する](../debugger/using-debuggertypeproxy-attribute.md)
- [ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)
- [デバッガー表示属性によるデバッグ機能の拡張](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
