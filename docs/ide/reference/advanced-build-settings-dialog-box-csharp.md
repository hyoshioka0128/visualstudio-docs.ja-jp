---
title: '[ビルドの詳細設定] ダイアログ ボックス (C#)'
ms.date: 08/05/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 917ef4ff685c243fa271a0966a931151cb12ed2b
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418848"
---
# <a name="advanced-build-settings-dialog-box-c"></a>[ビルドの詳細設定] ダイアログ ボックス (C#)

**プロジェクト デザイナー**の **[ビルドの詳細設定]** ダイアログ ボックスを使用して、プロジェクトの詳細なビルド構成プロパティを指定します。 このダイアログ ボックスは、C# プロジェクトにのみ適用されます。

## <a name="general"></a>全般

次のオプションを使用すると、全般的な詳細設定を有効にできます。

**言語バージョン**

::: moniker range=">=vs-2019"

[/langversion (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option) のリンク。プロジェクトのターゲット フレームワークに基づいて既定の言語バージョンが選択されるしくみに関する情報が提供されます。

::: moniker-end

::: moniker range="vs-2017"

使用する言語のバージョンを指定します。 機能セットはバージョンによって異なるので、このオプションを使用して、コンパイラが特定の実装機能のみを許可するように強制したり、既存の標準と互換性のある機能のみを有効にしたりすることができます。

既定値は C# 7.0 です。

::: moniker-end

**内部コンパイル エラー報告**

コンパイラ エラーを Microsoft に報告するかどうかを指定します。 **prompt** (既定) に設定すると、内部コンパイラ エラーが発生した場合にプロンプトが表示され、エラー報告を電子的に Microsoft に送信するオプションが示されます。 **send** に設定すると、エラー報告は自動的に送信されます。 **queue** に設定すると、報告はキューに追加されます。 **none** に設定すると、エラーはコンパイラのテキスト出力にのみ報告されます。 詳しくは、「[/errorreport (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option)」をご覧ください。

**演算のオーバーフローおよびアンダーフローのチェック**

[checked](/dotnet/csharp/language-reference/keywords/checked) キーワードまたは [unchecked](/dotnet/csharp/language-reference/keywords/unchecked) キーワードのスコープ内に含まれない整数の算術ステートメントと、データ型の範囲外の値になる整数の算術ステートメントで、ランタイム例外が発生するかどうかを指定します。 詳しくは、「[/checked (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option)」をご覧ください。

**標準ライブラリ (mscorlib.dll) を参照しない**

<xref:System> 名前空間全体を定義して、mscorlib.dll をプログラムにインポートするかどうかを指定します。 独自の <xref:System> 名前空間およびオブジェクトを定義または作成する場合は、このチェック ボックスをオンにします。 詳しくは、「[/nostdlib (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option)」をご覧ください。

## <a name="output"></a>Output

次のオプションを使用すると、詳細な出力オプションを指定できます。

**デバッグ情報**

コンパイラによって生成されるデバッグ情報の種類を指定します。 アプリケーションのデバッグ パフォーマンスを構成する方法については、「[イメージのデバッグの簡略化](/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug)」を参照してください。 この設定には、次のオプションがあります。

- **none**

   デバッグ情報を生成しないことを指定します。

- **full**

   実行中のプログラムにデバッガーをアタッチできるようにします。

- **pdbonly**

   プログラムがデバッガーで開始されたとき、ソース コードのデバッグが有効になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブラーが表示されます。

- **ポータブル**

   プラットフォーム固有ではない、移植可能なシンボル ファイルである .PDB ファイルを生成します。このファイルは、他のツール、特にデバッガーに、主要な実行可能ファイルの内容やそれが作られた経緯に関する情報を提供します。 詳細については、「[ポータブル PDB](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)」を参照してください。

- **埋め込み**

   ポータブル シンボル情報をアセンブリに埋め込みます。 外部 .PDB ファイルは作成されません。

詳しくは、「[/debug (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)」をご覧ください。

**ファイルの配置**

出力ファイル内のセクションのサイズを指定します。 有効値は **512**、**1024**、**2048**、**4096**、および **8192** です。 これらの値の単位はバイトです。 各セクションは、この値の倍数である境界内にアラインされるので、出力ファイルのサイズに影響があります。 詳しくは、「[/filealign (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option)」をご覧ください。

**ライブラリ ベース アドレス**

DLL を読み込む位置に推奨されるベース アドレスを指定します。 DLL の既定のベース アドレスは、.NET Framework 共通言語ランタイムにより設定されます。 詳しくは、「[/baseaddress (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option)」をご覧ください。

## <a name="see-also"></a>参照

- [C# コンパイラ オプション](/dotnet/csharp/language-reference/compiler-options/index)
- [[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)
