---
title: WPF .Targets ファイル | Microsoft Docs
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: adac07fff84bf0a447875b7084a3003e61a9767d
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578173"
---
# <a name="wpf-targets-files"></a>WPF .targets ファイル
[!INCLUDE[TLA#tla_winclient](../misc/includes/tlasharptla_winclient_md.md)] は、組み合わせて特殊な *.targets* ファイルである *Microsoft.WinFX.targets* が生成される [!INCLUDE[TLA2#tla_wpf](../msbuild/includes/tla2sharptla_wpf_md.md)] 固有のタスク セットを追加することで [!INCLUDE[TLA#tla_msbuild](../msbuild/includes/tlasharptla_msbuild_md.md)] を拡張します。 このファイルは、[!INCLUDE[TLA#tla_winclient](../misc/includes/tlasharptla_winclient_md.md)] で [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] プロジェクトを作るために必要な [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] タスクのセットを組み合わせます。

## <a name="see-also"></a>関連項目
- [MSBuild .targets ファイル](../msbuild/msbuild-dot-targets-files.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)