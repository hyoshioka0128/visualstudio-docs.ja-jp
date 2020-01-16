---
title: 複数バージョン対応プロジェクト
description: このドキュメントでは、Visual Studio for Mac で複数バージョン対応プロジェクトをセットアップする方法の概要について説明します。
ms.topic: overview
author: jmatthiesen
ms.author: jomatthi
ms.date: 12/12/2019
ms.assetid: 2a561af4-f1fe-493e-9a53-aa6d77d15498
ms.openlocfilehash: 3d1372ab5bd08ce164352293ec9d341ca567e3d5
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75439044"
---
# <a name="projects-with-multiple-target-frameworks"></a>複数のターゲット フレームワークを持つプロジェクト
Visual Studio for Mac では、いくつかの .NET Framework バージョンのいずれか、またはいくつかのシステム プラットフォームのいずれかで実行できるように、Xamarin または .NET Core プロジェクトを構成できます。 たとえば、.NET Framework 4.6 と .NET Core 3.1 の両方で実行できるように、プロジェクトのターゲットを設定することができます。 

ターゲット フレームワークの詳細については、「[ターゲット フレームワーク](/dotnet/standard/frameworks)」を参照してください。

> [!NOTE] 
> このトピックは、Visual Studio for Mac に適用されます。 Windows 上の Visual Studio については、「[フレームワーク対象設定機能の概要](/visualstudio/ide/visual-studio-multi-targeting-overview)」をご覧ください。

## <a name="targeting-multiple-frameworks"></a>複数のフレームワークをターゲットにする

ターゲット フレームワークはプロジェクト ファイル内で指定されます。これを編集するには、プロジェクトを右クリックし、 **[ツール] > [ファイルの編集]** コマンドを選択します。 単一のターゲット フレームワークを指定するときは、TargetFramework 要素を使います。 次のコンソール アプリのプロジェクト ファイルでは、.NET Core 3.0 をターゲットにする方法が示されています。

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>
```

ターゲット フレームワークが複数あるときは、複数形の TargetFrameworks 要素を使います。

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>
```

詳細については、[複数のフレームワークをターゲットにする](/dotnet/standard/frameworks#how-to-specify-target-frameworks)方法をご覧ください。

## <a name="working-with-code-in-a-multi-target-project"></a>複数バージョン対応プロジェクトでのコードの操作
複数のターゲット フレームワークを持つプロジェクトの C# ファイルを編集する場合は、使用するターゲット フレームワークを指定して、ご自分のエディター操作をガイドすることができます (たとえば、そのフレームワークでサポートされていない API を使用すると警告を表示します)。 ターゲット フレームワークを変更するには、エディター ウィンドウの左上隅にある **[ターゲット フレームワーク]** セレクターを使用します。

![ターゲット フレームワーク セレクターを使用して、ターゲット フレームワークを変更する (エディター ウィンドウの上部)](media/project-multitargeting-framework-selector.png)

場合によっては、お使いのアプリケーションのターゲット プラットフォームに応じて、異なる API を呼び出す必要があります。 これを行うには、条件コードを記述して、特定のプラットフォームに向けたコードをコンパイルします。

```C#
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45  
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

コードを記述するときに、IntelliSense のオートコンプリート候補に警告が表示されるため、お使いのアプリケーションがサポートしているターゲット フレームワークに対して特定の API が不足していないかどうかを確認できます。

![IntelliSense に表示される警告メッセージ。指定されたターゲット フレームワークに対して API が機能しません。 テキストの例: 名前空間 System.Buffers、SharedUtils (netstandard2.0) - 使用できません。 ナビゲーション バーを使用してコンテキストを切り替えることができます。](media/project-multitargeting-intellisense-warnings.png)

## <a name="see-also"></a>関連項目

- [フレームワーク対象設定機能の概要 (Windows)](/visualstudio/ide/visual-studio-multi-targeting-overview)
- [SDK スタイルのプロジェクトでのターゲット フレームワーク](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
