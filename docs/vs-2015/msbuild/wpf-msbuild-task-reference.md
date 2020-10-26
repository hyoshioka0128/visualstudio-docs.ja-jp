---
title: WPF MSBuild タスク リファレンス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eb21495954801d55c1db0bb9156a813ab73db683
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687093"
---
# <a name="wpf-msbuild-task-reference"></a>WPF MSBuild タスク リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Presentation Foundation (WPF) のビルド プロセスは、マークアップのコンパイルやリソースのプロセスを含む追加のビルド タスクのセットで Microsoft ビルド エンジン (MSBuild) を拡張します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [FileClassifier](../msbuild/fileclassifier-task.md)  
 ソース リソースのセットをアセンブリに埋め込まれるリソースとして分類します。 ローカライズできないリソースは、メイン アプリケーション アセンブリに埋め込まれます。ローカライズ可能なリソースは、サテライト アセンブリに埋め込まれます。  
  
 [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)  
 プロジェクト内の少なくとも 1 つの [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] ページが、そのプロジェクトでローカルに宣言されている型を参照している場合に、アセンブリを生成します。 生成されたアセンブリは、ビルド処理が完了した後、またはビルド処理が失敗した場合に削除されます。  
  
 [GetWinFXPath](../msbuild/getwinfxpath-task.md)  
 現在の [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] ランタイムのディレクトリを返します。  
  
 [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md)  
 ローカライズできない [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] プロジェクト ファイルをコンパイルされたバイナリ形式に変換します。  
  
 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)  
 同じプロジェクト内で型を参照する [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] ファイルの 2 回目のマークアップのコンパイルを実行します。  
  
 [MergeLocalizationDirectives](../msbuild/mergelocalizationdirectives-task.md)  
 1 つ以上の [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] バイナリ形式ファイルのローカリゼーション属性とコメントを、アセンブリ全体で単一のファイルにマージします。  
  
 [ResourcesGenerator](../msbuild/resourcesgenerator-task.md)  
 1 つ以上のリソース (.jpg、.ico、.bmp、バイナリ形式の [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)]、その他の種類の拡張子) を .resources ファイルに埋め込みます。  
  
 [UidManager](../msbuild/uidmanager-task.md)  
 ソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルに含まれるすべての [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 要素をローカライズするために、一意識別子 (UID) をチェック、更新、または削除します。  
  
 [UpdateManifestForBrowserApplication](../msbuild/updatemanifestforbrowserapplication-task.md)  
 **\<hostInBrowser />** プロジェクトのビルド時に、アプリケーションマニフェスト (*projectname*. .manifest) に要素を追加し [!INCLUDE[TLA#tla_xbap](../includes/tlasharptla-xbap-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)
