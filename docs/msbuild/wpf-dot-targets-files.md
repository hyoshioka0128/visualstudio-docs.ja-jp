---
title: WPF .Targets ファイル | Microsoft Docs
description: Windows Presentation Foundation (WPF) で、WPF 固有のタスク セットを特殊な .targets ファイル (Microsoft.WinFX.targets) に追加することによって、MSBuild を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- combining tasks into a .targets file to build an MSBuild project [WPF MSBuild]
- WPF .targets files [WPF MSBuild], introduction
- WPF .targets files [WPF MSBuild]
ms.assetid: e85a3ff4-dedd-4ff4-9b22-3a1e94755362
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a010ce3ff090b50557bedb62b7a611705fb9638a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933768"
---
# <a name="wpf-targets-files"></a>WPF .targets ファイル

Windows Presentation Foundation (WPF) によって、WPF 固有のタスク セットを追加することで MSBuild が拡張されます。このセットは、特殊な *.targets* ファイルである *Microsoft.WinFX.targets* にまとめられます。 このファイルにより、WPF で MSBuild プロジェクトを作成するために必要な MSBuild タスクのセットが組み合わされます。

## <a name="see-also"></a>関連項目

- [MSBuild .targets ファイル](../msbuild/msbuild-dot-targets-files.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)