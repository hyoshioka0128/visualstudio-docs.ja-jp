---
title: ファイルのビルド ファイル
description: Visual Studio プロジェクトのすべてのファイルにビルド アクションが含まれ、そのビルド アクションによって、プロジェクトのコンパイル時にファイルに行われる処理が制御されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/19/2018
ms.technology: vs-ide-compile
ms.topic: reference
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8884eaa459fa3a2a7dd8d10f0ffeca5003398afd
ms.sourcegitcommit: c9a84e6c01e12ccda9ec7072dd524830007e02a3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92136733"
---
# <a name="build-actions"></a>ビルド アクション

Visual Studio プロジェクト内のすべてのファイルに、ビルド アクションがあります。 ビルド アクションでは、プロジェクトのコンパイル時にファイルに行われる処理が制御されます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのビルド アクション](/visualstudio/mac/build-actions)に関するページを参照してください。

## <a name="set-a-build-action"></a>ビルド アクションを設定する

ファイルのビルド アクションを設定するには、 **[プロパティ]** ウィンドウでファイルのプロパティを開きます。その場合、 **ソリューション エクスプローラー** でファイルを選択し、 **Alt**+**Enter** キーを押します。 または、 **ソリューション エクスプローラー** でファイルを右クリックし、 **[プロパティ]** を選択します。 **[プロパティ]** ウィンドウの **[詳細設定]** セクションで、 **[ビルド アクション]** の横にあるドロップダウン リストを使用して、ファイルのビルド アクションを設定します。

![Visual Studio のファイルのビルド アクション](media/build-actions.png)

## <a name="build-action-values"></a>ビルド アクションの値

C# および Visual Basic プロジェクト ファイルの一般的なビルド アクションをいくつか以下に示します。

|ビルド アクション | プロジェクトの種類 | 説明 |
|-|-|
| **AdditionalFiles** | C#、Visual Basic | 入力として C# または Visual Basic コンパイラに渡される、ソース以外のテキスト ファイル。 このビルド アクションは主に、コードの品質を確認するためにプロジェクトによって参照される、[アナライザー](../code-quality/roslyn-analyzers-overview.md)への入力を提供するために使用されます。 詳細については、[追加ファイルの使用](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Using%20Additional%20Files.md)に関するページを参照してください。|
| **ApplicationDefinition** | WPF | アプリケーションが定義されているファイル。 最初にプロジェクトを作成したときは、これは *App.xaml* です。 |
| **CodeAnalysisDictionary** | .NET | スペル チェックのためにコード分析によって使用されるカスタム単語辞書。 「[方法:コード分析辞書をカスタマイズする](../code-quality/how-to-customize-the-code-analysis-dictionary.md)」を参照してください|
| **Compile** | any | ファイルはソース ファイルとしてコンパイラに渡されます。|
| **コンテンツ** | .NET | **Content** としてマークされたファイルは、<xref:System.Windows.Application.GetContentStream%2A?displayProperty=nameWithType> を呼び出すことでストリームとして取得できます。 ASP.NET プロジェクトの場合、展開時に、これらのファイルはサイトの一部として含まれます。|
| **DesignData** | WPF | デザイン時にユーザー コントロールをダミーの型とサンプル データを使用して表示できるようにするために、XAML ViewModel ファイルに使用されます。 |
| **DesignDataWithDesignTimeCreateable** | WPF | **DesignData** に似ていますが、実際の型が使用されます。  |
| **Embedded Resource** | .NET | ファイルは、アセンブリに埋め込むリソースとしてコンパイラに渡されます。 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A?displayProperty=fullName> を呼び出し、アセンブリからファイルを読み取ることができます。|
| **EntityDeploy** | .NET | Entity Framework (EF) の場合、EF 成果物の配置を指定する .edmx ファイル。 |
| **Fakes** | .NET | Microsoft Fakes テスト フレームワークに使用されます。 「[Microsoft Fakes を使用したテストでコードを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md)」をご覧ください |
| **なし** | any | ファイルはいかなる形でもビルドに含まれません。 この値は、"ReadMe" ファイルなどのドキュメント ファイルで使用できます。|
| **ページ** | WPF | 実行時の読み込みを高速化するために、XAML ファイルをバイナリの .baml ファイルとしてコンパイルします。 |
| **リソース** | WPF | 拡張子が *.g.resources* のアセンブリ マニフェスト リソース ファイルにファイルを埋め込むように指定します。 |
| **Shadow** | .NET | ビルド済みアセンブリ ファイル名のリストを含む .accessor ファイルに使用されます (1 行に 1 つ)。 リストのアセンブリごとに、元と同じ `ClassName_Accessor` という名前でパブリック クラスが生成されますが、プライベート メソッドではなくパブリック メソッドです。 単体テストに使用されます。 |
| **スプラッシュ スクリーン** | WPF | 実行時のアプリ起動時に表示される画像ファイルを指定します。 |
| **XamlAppDef** | Windows Workflow Foundation | ワークフローが埋め込まれたアセンブリとしてワークフロー XAML ファイルをビルドするよう、ビルドに指示します。 |

> [!NOTE]
> 特定のプロジェクトの種類に対して追加のビルド アクションを定義して、ビルドア クションのリストをプロジェクトの種類に基づくものにして、このリストに含まれない値が表示されるようにすることができます。

## <a name="see-also"></a>関連項目

- [C# コンパイラ オプション](/dotnet/csharp/language-reference/compiler-options/listed-alphabetically)
- [Visual Basic コンパイラ オプション](/dotnet/visual-basic/reference/command-line-compiler/compiler-options-listed-alphabetically)
- [ビルド アクション (Visual Studio for Mac)](/visualstudio/mac/build-actions)
