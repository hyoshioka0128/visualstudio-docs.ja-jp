---
title: .NET Framework を対象とするエラーのトラブルシューティング | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.FrameworkTargetingErrors
- MSBuild.ResolveAssemblyReference.FailedToResolveReferenceBecausePrimaryAssemblyInExclusionList
helpviewer_keywords:
- targeting .NET Framework version [Visual Studio]
- versions [Visual Studio], .NET Framework Client Profile
- multi-targeting
- multitargeting
- .NET Framework Client Profile
ms.assetid: 830e3e45-9a93-4279-a249-75b84599aefb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1c384f7e2bdd22f7a68140c90aa172d1efc9aca6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594917"
---
# <a name="troubleshoot-net-framework-targeting-errors"></a>.NET Framework を対象とするエラーのトラブルシューティング
このトピックは、参照の問題が原因で発生する可能性のある MSBuild エラーと、そのエラーの解決方法について説明します。

## <a name="you-have-referenced-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>異なるバージョンの .NET Framework を対象とするプロジェクトまたはアセンブリを参照した
 異なるバージョンの .NET Framework を対象にしたプロジェクトまたはアセンブリを参照するアプリケーションを作成できます。 たとえば、.NET Framework 4 のクライアント プロファイルを対象とするが、.NET Framework 2.0 を対象とするアセンブリを参照するアプリケーションを作成できます。 ただし、以前のバージョンの .NET Framework を対象とするプロジェクトを作成した場合、そのプロジェクトでは、.NET Framework 4 のクライアント プロファイルまたは .NET Framework 4 自体を対象とするプロジェクトまたはアセンブリに参照を設定することはできません。 エラーを解決するには、アプリケーションで参照されるプロジェクトまたはアセンブリが対象とするプロファイルと互換性のあるプロファイルがアプリケーションの対象となるようにします。

## <a name="you-have-re-targeted-a-project-to-a-different-version-of-the-net-framework"></a>異なるバージョンの .NET Framework にプロジェクトの対象を再設定した
 アプリケーションの .NET Framework のターゲット バージョンを変更する場合、Visual Studio で変更される参照もあれば、手動による更新が必要な参照もあります。 たとえば、[!INCLUDE[net_v35SP1_long](../msbuild/includes/net_v35sp1_long_md.md)] を対象とするようにアプリケーションを変更する際に、そのアプリケーションのリソースまたは設定が .NET Framework 4 のクライアント プロファイルに依存している場合は、前述のエラーのいずれかが発生する可能性があります。

 このようなアプリケーションの設定に対処するには、**ソリューション エクスプローラー**を開き、 **[すべてのファイルを表示]** を選択してから、Visual Studio の XML エディターで *app.config* ファイルを編集します。 .NET Framework の適切なバージョンと一致するように、設定されているバージョンを変更します。 たとえば、バージョンの設定を 4.0.0.0 から 2.0.0.0 に変更できます。 同様に、リソースを追加したアプリケーションでは、**ソリューション エクスプローラー**を開き、 **[すべてのファイルを表示]** ボタンを選択し、 **[マイ プロジェクト]** (Visual Basic の場合) または **[プロパティ]** (C# の場合) を展開してから Visual Studio の XML エディターで *Resources.resx* ファイルを編集します。 バージョンの設定を 4.0.0.0 から 2.0.0.0 に変更します。

 アプリケーションにアイコンやビットマップなどのリソースまたはデータ接続文字列などの設定が含まれている場合は、**プロジェクト デザイナー**の **[設定]** ページですべての項目を削除してから、必要な設定を再度追加することで、エラーを解決することもできます。

## <a name="you-have-re-targeted-a-project-to-a-different-version-of-the-net-framework-and-references-do-not-resolve"></a>異なるバージョンの .NET Framework にプロジェクトの対象を再設定したが、参照が解決されない
 異なるバージョンの .NET Framework にプロジェクトの対象を再設定した場合に、参照が正しく解決されないことがあります。 多くの場合、アセンブリへの明示的な完全修飾参照によってこの問題が発生しますが、解決されない参照を削除してからプロジェクトに追加し直すことで解決できます。 あるいは、参照を置き換えるようにプロジェクト ファイルを編集することもできます。 まず、以下のフォームの参照を削除します。

```xml
<Reference Include="System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089, processorArchitecture=MSIL" />
```

 次に、以下の単純なフォームに置き換えます。

```xml
<Reference Include="System.ServiceModel" />
```

> [!NOTE]
> プロジェクトを閉じて再び開いてから、リビルドし、すべての参照が正しく解決されるようにする必要もあります。

## <a name="see-also"></a>関連項目

- [方法: .NET Framework のバージョンをターゲットにする](../ide/visual-studio-multi-targeting-overview.md)
- [.NET Framework クライアント プロファイル](/dotnet/framework/deployment/client-profile)
- [フレームワーク対象設定機能の概要](../ide/visual-studio-multi-targeting-overview.md)
- [マルチ ターゲット](../msbuild/msbuild-multitargeting-overview.md)
