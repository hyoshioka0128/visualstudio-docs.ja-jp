---
title: 対象の .NET Framework
ms.date: 02/06/2018
ms.topic: conceptual
helpviewer_keywords:
- targeting .NET Framework [Visual Studio]
- framework targeting [Visual Studio]
- .NET framework targeting [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ec81b38ab68c327f25c9f94b6329a700e2662383
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307329"
---
# <a name="framework-targeting-overview"></a>フレームワーク対象設定機能の概要

Visual Studio では、プロジェクトの対象となる .NET のバージョンを指定できます。 フレームワークを対象にする機能は、指定したフレームワーク バージョンで利用できる機能のみをアプリケーションで使用することを保証するのに役立ちます。 別のコンピューター上で実行する .NET Framework アプリについては、アプリケーションが対象とする .NET Framework バージョンが、コンピューターにインストールされている .NET Framework バージョンとの互換性を持っている必要があります。

Visual Studio のソリューションには、異なるバージョンの .NET を対象とするプロジェクトを含めることができます。

ターゲット フレームワークの詳細については、「[ターゲット フレームワーク](/dotnet/standard/frameworks)」を参照してください。

> [!TIP]
> 異なるプラットフォームに対応する複数のアプリケーションを対象にすることもできます。 詳細については、[MSBuild のマルチ ターゲット](../msbuild/msbuild-multitargeting-overview.md)に関する記事をご覧ください。

## <a name="framework-targeting-features"></a>フレームワークの対象設定機能

フレームワークの対象設定機能には、次の特徴があります。

- 旧フレームワーク バージョンを対象とするプロジェクトを開いたときに、Visual Studio でそのプロジェクトを自動的にアップグレードするか、前のバージョンを対象とした状態を維持することができます。

- .NET Framework プロジェクトを作成するときに、対象とする .NET Framework のバージョンを指定できます。

- 1 つのプロジェクトで[複数のフレームワークをターゲットに設定](/dotnet/standard/frameworks#how-to-specify-target-frameworks)できます。

- 同じソリューション内にある複数のプロジェクトのそれぞれで、異なるバージョンの .NET を対象とすることができます。

- 既存のプロジェクトの対象となっている .NET のバージョンを変更できます。

   プロジェクトの対象となる .NET のバージョンを変更すると、Visual Studio では、参照ファイルおよび構成ファイルに対して必要な変更が加えられます。

以前のフレームワーク バージョンを対象とするプロジェクトで作業するとき、Visual Studio では、開発環境が次のように動的に変更されます。

- **[新しい項目の追加]** 、 **[新しい参照の追加]** 、 **[サービス参照の追加]** の各ダイアログ ボックスの項目をフィルター処理して、対象のバージョンで使用できない選択肢を除外します。

- **ツールボックス**内のカスタム コントロールをフィルター処理し、対象のバージョンで使用できないコントロールを除外したり、複数のコントロールが使用可能である場合に最新のコントロールのみを表示したりします。

- **IntelliSense** をフィルター処理して、対象のバージョンで使用できない言語機能を除外します。

- **プロパティ** ウィンドウのプロパティをフィルター処理して、対象のバージョンで使用できないプロパティを除外します。

- メニュー オプションをフィルター処理して、対象のバージョンで使用できないオプションを除外します。

- ビルドを行う場合は、対象のバージョンに適したコンパイラのバージョンおよびコンパイラ オプションを使用します。

> [!NOTE]
> - フレームワークの対象機能は、開発中のアプリケーションが正しく実行されることを保証するわけではありません。 対象のバージョンで実行できるかどうかを確認するために、アプリケーションをテストする必要があります。
> - .NET Framework 2.0 より前のバージョンのフレームワークを対象にすることはできません。

## <a name="select-a-target-framework-version"></a>対象フレームワークのバージョンを選択する

.NET Framework プロジェクトを作成するときは、プロジェクト テンプレートを選択した後で、対象の .NET Framework バージョンを選択できます。 使用できる Framework のリストには、選択したテンプレートの種類に適用されるインストール済みの Framework バージョンが表示されます。 .NET Core テンプレート、.NET Framework 以外のプロジェクト テンプレートの場合、 **[Framework]** ドロップダウン リストは表示されません。

::: moniker range="vs-2017"

![VS 2017 でのフレームワーク ドロップダウン](media/vside-newproject-framework.png)

::: moniker-end

::: moniker range=">=vs-2019"

![VS 2019 でのフレームワーク ドロップダウン](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="change-the-target-framework"></a>ターゲット フレームワークを変更する

Visual Basic、C#、または F# の既存のプロジェクトでは、プロジェクトのプロパティ ダイアログ ボックスで、.NET のターゲット バージョンを変更します。 C++ プロジェクトのターゲット バージョンを変更する方法については、代わりに「[How to: Modify the Target Framework and Platform Toolset (方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)」をご覧ください。

1. **ソリューション エクスプローラー**で、変更するプロジェクトの右クリック メニューを開き、 **[プロパティ]** を選択します。

1. **[プロパティ]** ウィンドウの左側の列で、 **[アプリケーション]** タブを選択します。

   ![プロジェクトのプロパティの [アプリケーション] タブ](../ide/media/vs_slnexplorer_properties_applicationtab.png)

   > [!NOTE]
   > UWP アプリを作成した後は、Windows または .NET のターゲット バージョンを変更することはできません。

1. **[ターゲット フレームワーク]** 一覧で、目的のバージョンを選択します。

1. 表示される検証ダイアログ ボックスで **[はい]** ボタンを選択します。

   プロジェクトがアンロードされます。 プロジェクトを再読み込みすると、上で選択した .NET のバージョンが対象になります。

> [!NOTE]
> 対象とするバージョンとは別の .NET のバージョンへの参照がコードに含まれている場合、コードをコンパイルまたは実行するとエラー メッセージが表示されることがあります。 これらのエラーを解決するには、参照を変更します。 「[.NET を対象とするエラーのトラブルシューティング](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)」を参照してください。

> [!TIP]
> ターゲット フレームワークによっては、プロジェクト ファイル内で次のように表現されている場合があります。
>
> - .NET Core アプリの場合: `<TargetFramework>netcoreapp2.1</TargetFramework>`
> - .NET Standard アプリの場合: `<TargetFramework>netstandard2.0</TargetFramework>`
> - .NET Framework アプリの場合: `<TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>`

## <a name="resolve-system-and-user-assembly-references"></a>システム参照およびユーザー アセンブリ参照の解決

.NET の特定のバージョンを対象にするには、最初に適切なアセンブリ参照をインストールする必要があります。 [.NET ダウンロード](https://www.microsoft.com/net/download/windows) ページでさまざまなバージョンの .NET の開発者向けパックをダウンロードすることができます。

.NET Framework プロジェクトの場合、 **[参照の追加]** ダイアログ ボックスでは、対象の .NET Framework のバージョンに関係しないシステム アセンブリが無効にされます。その結果、それらのアセンブリをプロジェクトに誤って追加することはありません。 (システム アセンブリとは、.NET Framework バージョンの一部である *.dll* ファイルのことです)。対象より新しいバージョンのフレームワークに属する参照は解決されず、そのような参照に依存するコントロールを追加することはできません。 このような参照を有効にするには、プロジェクトの対象である .NET Framework を、その参照を含むバージョンに再設定します。

アセンブリ参照の詳細については、「[デザイン時のアセンブリの解決](../msbuild/resolving-assemblies-at-design-time.md)」を参照してください。

## <a name="enable-linq"></a>LINQ を有効にする

.NET Framework Version 3.5 以降を対象にする場合は、**System.Core** の参照と <xref:System.Linq> のプロジェクトレベル インポート (Visual Basic のみ) が自動的に追加されます。 LINQ 機能を使用する場合は、`Option Infer` もオンにする必要があります (Visual Basic のみ)。 対象をそれより前のバージョンの .NET Framework に変更すると、この参照とインポートは自動的に削除されます。 詳細については、「[LINQ の使用](/dotnet/csharp/tutorials/working-with-linq)」を参照してください。

## <a name="see-also"></a>関連項目

- [ターゲット フレームワーク](/dotnet/standard/frameworks)
- [マルチ ターゲット (MSBuild)](../msbuild/msbuild-multitargeting-overview.md)
- [方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する (C++)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)
