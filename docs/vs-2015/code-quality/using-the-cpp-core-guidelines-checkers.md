---
title: C++ Core Guidelines のチェッカー | を使用するMicrosoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: a2098fd9-8334-4e95-9b8d-bc3da689d9e3
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: fffa4cec6a2bd7a340b90776ac20dc486f28045b
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173558"
---
# <a name="using-the-c-core-guidelines-checkers"></a>C++ Core ガイドライン チェッカーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C++ Core Guidelines は、C++ の専門家とデザイナーによって作成された C++ のコーディングに関するガイドライン、規則、およびベストプラクティスの移植可能なセットです。  Visual Studio では、コード分析ツールに対して追加のルールを作成して C++ Core Guidelines に準拠しているかどうかを確認し、改善を提案するアドインパッケージがサポートされるようになりました。  
  
## <a name="the-c-core-guidelines-project"></a>C++ Core Guidelines プロジェクト  
 Bjarne Stroustrup などによって作成された C++ Core Guidelines は、最新の C++ を安全かつ効果的に使用するためのガイドです。 このガイドラインでは、静的なタイプセーフとリソースの安全性を重視しています。 これらの例では、言語のエラーが発生しやすい部分を排除または最小化する方法を示し、信頼性の高い方法でコードをより簡単かつ効率的にする方法を提案します。 これらのガイドラインは、標準 C++ Foundation によって管理されています。 詳細については、ドキュメントを参照し、 [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)して、 [GitHub](https://github.com/isocpp/CppCoreGuidelines)の C++ Core Guidelines ドキュメントプロジェクトファイルにアクセスしてください。  
  
 Microsoft では、Nuget パッケージを使用してプロジェクトに追加できる C++ Core Check コード分析規則セットを作成することによって、C++ Core Guidelines の作業をサポートしています。 パッケージは CppCoreCheck という名前で、で入手でき [https://www.nuget.org/packages/Microsoft.CppCoreCheck](https://www.nuget.org/packages/Microsoft.CppCoreCheck) ます。 このパッケージには、少なくとも Visual Studio 2015 with Update 1 がインストールされている必要があります。  
  
 また、パッケージは、ヘッダーのみのガイドラインサポートライブラリ (GSL) である依存関係として別のパッケージをインストールします。 GSL は、GitHub のでも参照でき [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL) ます。  
  
## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>コード分析での C++ Core Check ガイドラインの有効化  
 C++ Core Check コード分析ツールを有効にするには、Visual Studio 内で確認する各 C++ プロジェクトに CppCoreCheck NuGet パッケージをインストールします。  
  
#### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project"></a>CppCoreCheck パッケージをプロジェクトに追加するには  
  
1. **ソリューションエクスプローラー**で、右クリックして、パッケージを追加するソリューション内のプロジェクトのコンテキストメニューを開きます。 [ **Nuget**パッケージの管理] を選択して、 **nuget パッケージマネージャー**を開きます。  
  
2. [ **NuGet パッケージマネージャー** ] ウィンドウで、CppCoreCheck を検索します。  
  
    ![Nuget パッケージマネージャーウィンドウに CppCoreCheck パッケージが表示されます](../code-quality/media/cppcorecheck-nuget-window.PNG "CPPCoreCheck_Nuget_Window")  
  
3. CppCoreCheck パッケージを選択し、[**インストール**] をクリックして、プロジェクトに規則を追加します。  
  
   NuGet パッケージは、プロジェクトに対してコード分析を有効にしたときに呼び出される追加の MSBuild. .targets ファイルをプロジェクトに追加します。 この .targets ファイルは、Visual Studio コード分析ツールに追加の拡張機能として C++ Core Check 規則を追加します。  
  
   プロジェクトのコード分析を有効にするには、プロジェクトの [**プロパティページ**] ダイアログの [**コード分析**] セクションで [**ビルド時にコード分析を有効にする**] チェックボックスをオンにします。  
  
   ![コード分析の全般設定のプロパティページ](../code-quality/media/cppcorecheck-codeanalysis-general.png "CPPCoreCheck_CodeAnalysis_General")  
  
   C++ Core Check 規則は、コード分析が有効になったときに実行される既定の規則セットの一部になります。 C++ Core Check の規則は開発中なので、一部の規則はすべてのコードで使用できるように準備されていない場合がありますが、開発時に役立つことがあります。 これらのルールは試験段階としてリリースされます。 プロジェクトのプロパティで、リリース済みまたは試験的な規則を実行するかどうかを選択できます。  
  
   ![コード分析拡張機能の設定のプロパティページ](../code-quality/media/cppcorecheck-codeanalysis-extensions.png "CPPCoreCheck_CodeAnalysis_Extensions")  
  
   C++ Core Check の規則セットを有効または無効にするには、プロジェクトの [**プロパティページ**] ダイアログを開きます。 [**構成プロパティ**] で、[**コード分析**]、[**拡張機能**] の順に展開します。 [ **C++ Core Check の有効化 (リリース)** ] または [C++ Core Check を有効にする **(試験段階)**] の横にあるドロップダウンコントロールで、[**はい]** または [**いいえ**] を選択します。 **[OK]** または [**適用**] を選択して、変更を保存します。  
  
## <a name="check-types-bounds-and-lifetimes"></a>型、境界、および有効期間のチェック  
 C++ Core Check パッケージには、現在、[タイプセーフ](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-type)、[境界の安全性](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-bounds)、および[有効期間の安全性](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-lifetime)のプロファイルのチェックが含まれています。  
  
 C++ Core Check の規則によって検出される可能性のある問題の例を次に示します。  
  
```cpp  
// CoreCheckExample.cpp  
// Add CppCoreCheck package and enable code analysis in build for warnings.  
  
int main()  
{  
    int arr[10];           // warning C26494  
    int* p = arr;          // warning C26485  
  
    [[gsl::suppress(bounds.1)]] // This attribute suppresses Bounds rule #1  
    {  
        int* q = p + 1;    // warning C26481 (suppressed)  
        p = q++;           // warning C26481 (suppressed)  
    }  
  
    return 0;  
}  
```  
  
 この例では、C++ Core Check の規則で検出できる警告のいくつかを示します。  
  
- C26494 は rule 型です。 5: 常にオブジェクトを初期化します。  
  
- C26485 はルールの境界です。 3: 配列からポインターへの減衰がありません。  
  
- C26481 は rule Bounds です。 1: ポインター演算は使用しないでください。 代わりに、`span` を使用してください。  
  
  このコードをコンパイルするときに C++ Core Check コード分析のルールセットがインストールされ、有効になっている場合、最初の2つの警告が出力されますが、3番目の警告は抑制されます。 コード例のビルド出力を次に示します。  
  
**1>------ビルドを開始しました: プロジェクト: CoreCheckExample、構成: デバッグ Win32--**  
**----**  
**1> CoreCheckExample .cpp**  
**1> CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.exe**  
**1> CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.pdb (完全な PDB)**  
**c:\users\username\documents\visual studio 2015 \ プロジェクト \ corecheckexample**  
**ckexample\corecheckexample.cpp (6): warning C26494: 変数 ' arr ' は uninitializ**  
**ed。常にオブジェクトを初期化します。(type .5: https: \/ /go.microsoft.com/fwlink/p/?Link**  
**ID = 620421)**  
**c:\users\username\documents\visual studio 2015 \ プロジェクト \ corecheckexample**  
**ckexample\corecheckexample.cpp (7): warning C26485: Expression ' arr ': 次に対する配列はありません**  
**ポインターの減衰。(境界 3: https: \/ /go.microsoft.com/fwlink/p/?LinkID=620415)**  
**========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========** 

C++ Core Guidelines は、より適切で安全なコードを記述するのに役立ちます。 ただし、ルールまたはプロファイルを適用できないインスタンスがある場合は、コード内で直接非表示にするのが簡単です。 属性を使用すると、 `gsl::suppress` 次のコードブロックの規則違反を検出して報告することが C++ Core Check によって防止されます。 個々のステートメントをマークして、特定のルールを抑制することができます。 `[[gsl::suppress(bounds)]]`特定の規則番号を含めずに、境界プロファイル全体を作成して抑制することもできます。  
  
## <a name="use-the-guideline-support-library"></a>ガイドラインサポートライブラリを使用する  
 また、CppCoreCheck NuGet パッケージでは、Microsoft によるガイドラインサポートライブラリ (GSL) の実装を含むパッケージもインストールされます。 GSL は、のスタンドアロン形式でも使用でき [http://www.nuget.org/packages/Microsoft.Gsl](https://www.nuget.org/packages/Microsoft.Gsl) ます。 このライブラリは、主要なガイドラインに従う場合に便利です。 GSL には、エラーが発生しやすい構造を代替として置き換えることができる定義が含まれています。 たとえば、 `T*, length` パラメーターのペアを型に置き換えることができ `span<T>` ます。 GSL はオープンソースであるため、ライブラリのソース、コメント、または投稿を確認する場合は、プロジェクトがにあり [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL) ます。
