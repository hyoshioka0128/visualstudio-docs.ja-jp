---
title: WPF MSBuild タスク リファレンス | Microsoft Docs
description: 追加のタスクを使用して MSBuild を拡張する Windows Presentation Foundation (WPF) のビルド プロセスに関するタスク リファレンスを確認します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 94050565e6c5619781434c7a18307bfbf80b51f9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933675"
---
# <a name="wpf-msbuild-task-reference"></a>WPF MSBuild タスク リファレンス

Windows Presentation Foundation (WPF) のビルド プロセスは、マークアップのコンパイルやリソースのプロセスを含む追加のビルド タスクのセットで Microsoft ビルド エンジン (MSBuild) を拡張します。

## <a name="in-this-section"></a>このセクションの内容

- [FileClassifier](../msbuild/fileclassifier-task.md)

 ソース リソースのセットをアセンブリに埋め込まれるリソースとして分類します。 ローカライズできないリソースは、メイン アプリケーション アセンブリに埋め込まれます。ローカライズ可能なリソースは、サテライト アセンブリに埋め込まれます。

- [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)

 プロジェクト内の少なくとも 1 つの XAML ページで、そのプロジェクトでローカルに宣言されている型が参照されている場合、アセンブリを生成します。 生成されたアセンブリは、ビルド処理が完了した後、またはビルド処理が失敗した場合に削除されます。

- [GetWinFXPath](../msbuild/getwinfxpath-task.md)

 現在の .NET Framework ランタイムのディレクトリを返します。

- [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md)

 ローカライズできない XAML プロジェクト ファイルをコンパイルされたバイナリ形式に変換します。

- [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)

 同じプロジェクト内で型を参照する XAML ファイルの 2 回目のマークアップのコンパイルを実行します。

- [MergeLocalizationDirectives](../msbuild/mergelocalizationdirectives-task.md)

 1 つ以上の XAML バイナリ形式ファイルのローカリゼーション属性とコメントを、アセンブリ全体で単一のファイルにマージします。

- [ResourcesGenerator](../msbuild/resourcesgenerator-task.md)

 1 つ以上のリソース ( *.jpg*、 *.ico*、 *.bmp*、バイナリ形式の XAML、その他の種類の拡張子) を *.resources* ファイルに埋め込みます。

- [UidManager](../msbuild/uidmanager-task.md)

 ソース XAML ファイルに含まれるすべての XAML 要素をローカライズするために、一意識別子 (UID) をチェック、更新、または削除します。

- [UpdateManifestForBrowserApplication](../msbuild/updatemanifestforbrowserapplication-task.md)

 XAML ブラウザー アプリケーション (XBAP) プロジェクトのビルド時に **\<hostInBrowser />** 要素をアプリケーション マニフェスト ( *\<projectname>.exe.manifest*) に追加します。

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)