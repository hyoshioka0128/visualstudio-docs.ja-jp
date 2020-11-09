---
title: MSBuild のマルチターゲットの概要 | Microsoft Docs
description: MSBuild を使用して、.NET Framework のいずれかのバージョンやいずれかのシステム プラットフォームで動作するように、アプリケーションをコンパイルする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: eecbcd65-9fbc-4307-a321-46d3c3b79b12
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47b4ba2c27e130580af961216739289c6c7e9585
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046307"
---
# <a name="msbuild-multitargeting-overview"></a>MSBuild のマルチ ターゲットの概要

MSBuild を使用すると、.NET Framework のいずれかのバージョンやいずれかのシステム プラットフォームで動作するように、アプリケーションをコンパイルできます。 たとえば、あるアプリケーションを 32 ビット プラットフォーム上の .NET Framework 2.0 で動作するようにコンパイルしたり、これと同じアプリケーションを 64 ビット プラットフォーム上の .NET Framework 4.5 で動作するようにコンパイルしたりできます。

> [!IMPORTANT]
> "マルチ ターゲット" という用語が使用されていますが、プロジェクトでは、一度に 1 つのフレームワークと 1 つのプラットフォームだけを対象にすることができます。

 MSBuild の機能の対象となるフレームワークやプラットフォームの一部を次に示します。

- バージョン 2.0、3.5、4 などの以前のバージョンの .NET Framework を対象とするアプリケーションを開発できます。

- Silverlight フレームワークなど、.NET Framework 以外のフレームワークを対象にできます。

- ターゲット フレームワークの定義済みのサブセットである *フレームワーク プロファイル* を対象にできます。

- 現在のバージョンの .NET Framework 用サービス パックがリリースされた場合、そのバージョンを対象にできます。

- MSBuild の対象となるフレームワークやプラットフォームで動作するアプリケーションでは、それらのフレームワークやプラットフォームで利用できる機能だけを使うことができます。

## <a name="target-framework-and-platform"></a>ターゲット フレームワークとターゲット プラットフォーム

 *ターゲット フレームワーク* は、ビルドされるプロジェクトの実行対象となる .NET Framework のバージョンを表します。また、 *ターゲット プラットフォーム* は、ビルドされるプロジェクトの実行対象となるシステム プラットフォームを表します。  たとえば、80x86 プロセッサ ファミリ (x86) と互換性のある 32 ビット プラットフォームで動作する .NET Framework 2.0 アプリケーションを対象とする場合があります。 ターゲット フレームワークとターゲット プラットフォームの組み合わせは *ターゲット コンテキスト* と呼ばれます。 詳細については、「[ターゲット フレームワークおよびターゲット プラットフォーム](../msbuild/msbuild-target-framework-and-target-platform.md)」を参照してください。

## <a name="toolset-toolsversion"></a>ツール セット (ToolsVersion)

 ツール セットには、アプリケーションの作成に使用されるツール、タスク、ターゲットがまとめられています。 ツールセットには、 *csc.exe* や *vbc.exe* などのコンパイラ、共通 targets ファイル ( *microsoft.common.targets* )、および共通 tasks ファイル ( *microsoft.common.tasks* ) が含まれています。 4\.5 ツールセットを使用すると、バージョン 2.0、3.0、3.5、4、4.5 の .NET Framework を対象とすることができます。 ただし、2.0 ツールセットは .NET Framework バージョン 2.0 のみを対象として使用できます。 詳細については、「[ツール セット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」を参照してください。

## <a name="reference-assemblies"></a>参照アセンブリ

 ツールセットで指定されている参照アセンブリは、アプリケーションの設計とビルドに役立ちます。 これらの参照アセンブリを利用すると、特定のターゲットのビルドが実行できるだけでなく、Visual Studio IDE のコンポーネントと機能を制限して、ターゲットと互換性のあるコンポーネントと機能のみを使用できるようになります。 詳細については、「[デザイン時のアセンブリの解決](../msbuild/resolving-assemblies-at-design-time.md)」を参照してください。

## <a name="configure-targets-and-tasks"></a>ターゲットとタスクを構成する

 MSBuild のターゲットとタスクを、MSBuild のアウトプロセスで実行するように構成できます。これにより、開発時に実行しているコンテキストとは異なるコンテキストを対象とすることができます。  たとえば、開発用コンピューターが .NET Framework 4.5 を備えた 64 ビット プラットフォームで動作している場合でも、32 ビットの .NET Framework 2.0 アプリケーションを対象とすることができます。 詳細については、「[ターゲットとタスクの構成](../msbuild/configuring-targets-and-tasks.md)」を参照してください。

## <a name="troubleshooting"></a>トラブルシューティング

 ターゲット コンテキストに含まれないアセンブリを参照しようとすると、エラーが発生する場合があります。 これらのエラーおよび対処方法の詳細については、「[.NET Framework を対象とするエラーのトラブルシューティング](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)」を参照してください。
