---
title: ビジュアライザー API リファレンス | Microsoft Docs
description: ビジュアライザーには、特定の種類のデータ要素が表示され、編集を許可することもできます。 作成するには、このセクションに記載されているビジュアライザー API を使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- APIs, visualizers
- reference, visualizer APIs
- visualizers, API reference
ms.assetid: b9ff4ed0-9e80-49df-9016-a81189319afd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b790bcdc11e80b8f01877efe4a8d9497038b260b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99884261"
---
# <a name="visualizer-api-reference"></a>ビジュアライザー API リファレンス

ビジュアライザー API は Visual Studio デバッガーのビジュアライザーを記述する必要のあるユーザー向けに用意されています。 ビジュアライザーは、Visual Studio デバッガー ユーザー インターフェイスの機能を拡張した小規模なアプリケーションです。 ビジュアライザーには、デザイン時に指定された特定タイプのデータ オブジェクトを表示 (およびオプションで編集) できます。

## <a name="in-this-section"></a>このセクションの内容

- <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerDevelopmentHost?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource?displayProperty=fullName>

## <a name="see-also"></a>関連項目

- [チュートリアル: C# でビジュアライザーを記述する](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [方法: ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)