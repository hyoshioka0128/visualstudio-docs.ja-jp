---
title: WPF MSBuild タスク リファレンス | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- WPF MSBuild task reference [WPF MSBuild], term/definition table
- build tasks [WPF MSBuild], Microsoft build engine
- build tasks using the Microsoft build engine [WPF MSBuild], compile markup and process resources
- WPF MSBuild task reference [WPF MSBuild]
ms.assetid: 96df0370-e50f-4ffc-9771-b12fb8721143
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 84aeae06a5440bfc82eb9590919800ebcdd425d5
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578192"
---
# <a name="wpf-msbuild-task-reference"></a>WPF MSBuild タスク リファレンス
Windows Presentation Foundation (WPF) のビルド プロセスは、マークアップのコンパイルやリソースのプロセスを含む追加のビルド タスクのセットで Microsoft ビルド エンジン (MSBuild) を拡張します。

## <a name="in-this-section"></a>このセクションの内容
- [FileClassifier](../msbuild/fileclassifier-task.md)

 ソース リソースのセットをアセンブリに埋め込まれるリソースとして分類します。 ローカライズできないリソースは、メイン アプリケーション アセンブリに埋め込まれます。ローカライズ可能なリソースは、サテライト アセンブリに埋め込まれます。

- [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)

 プロジェクト内の少なくとも 1 つの [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] ページが、そのプロジェクトでローカルに宣言されている型を参照している場合に、アセンブリを生成します。 生成されたアセンブリは、ビルド処理が完了した後、またはビルド処理が失敗した場合に削除されます。

- [GetWinFXPath](../msbuild/getwinfxpath-task.md)

 現在の [!INCLUDE[TLA#tla_winfx](../msbuild/includes/tlasharptla_winfx_md.md)] ランタイムのディレクトリを返します。

- [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md)

 ローカライズできない [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] プロジェクト ファイルをコンパイルされたバイナリ形式に変換します。

- [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)

 同じプロジェクト内で型を参照する [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] ファイルの 2 回目のマークアップのコンパイルを実行します。

- [MergeLocalizationDirectives](../msbuild/mergelocalizationdirectives-task.md)

 1 つ以上の [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] バイナリ形式ファイルのローカリゼーション属性とコメントを、アセンブリ全体で単一のファイルにマージします。

- [ResourcesGenerator](../msbuild/resourcesgenerator-task.md)

 1 つ以上のリソース ( *.jpg*、 *.ico*、 *.bmp*、バイナリ形式の [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)]、その他の種類の拡張子) を *.resources* ファイルに埋め込みます。

- [UidManager](../msbuild/uidmanager-task.md)

 ソース [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] ファイルに含まれるすべての [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] 要素をローカライズするために、一意識別子 (UID) をチェック、更新、または削除します。

- [UpdateManifestForBrowserApplication](../msbuild/updatemanifestforbrowserapplication-task.md)

 [!INCLUDE[TLA#tla_xbap](../msbuild/includes/tlasharptla_xbap_md.md)] プロジェクトのビルド時に **\<hostInBrowser />** 要素をアプリケーション マニフェスト ( *\<プロジェクト名>.exe.manifest*) に追加します。

## <a name="see-also"></a>関連項目
- [MSBuild](../msbuild/msbuild.md)