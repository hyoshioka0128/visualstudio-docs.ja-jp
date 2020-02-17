---
title: コアガイドラインC++チェッカーの使用 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: a2098fd9-8334-4e95-9b8d-bc3da689d9e3
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 946b46bfb5101154832e10b61cd861b0c104dc14
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77275303"
---
# <a name="using-the-c-core-guidelines-checkers"></a>C++ Core ガイドライン チェッカーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C++コアガイドラインは、専門家や設計者によってC++ C++作成されたコーディングに関するガイドライン、ルール、およびベストプラクティスの移植可能なセットです。  Visual Studio では、コード分析ツールに対して追加のルールを作成して、 C++コアガイドラインに準拠しているかどうかを確認し、改善を提案するアドインパッケージがサポートされるようになりました。  
  
## <a name="the-c-core-guidelines-project"></a>C++コアガイドラインプロジェクト  
 Bjarne Stroustrup によって作成されC++たコアガイドラインは、最新C++の安全かつ効果的に使用するためのガイドです。 このガイドラインでは、静的なタイプセーフとリソースの安全性を重視しています。 これらの例では、言語のエラーが発生しやすい部分を排除または最小化する方法を示し、信頼性の高い方法でコードをより簡単かつ効率的にする方法を提案します。 これらのガイドラインは、Standard C++ Foundation によって管理されています。 詳細については、 [GitHub](https://github.com/isocpp/CppCoreGuidelines)のドキュメントと[ C++コアガイドライン](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)を参照C++し、主要ガイドラインドキュメントプロジェクトファイルにアクセスしてください。  
  
 Microsoft ではC++ 、Nuget パッケージを使用C++してプロジェクトに追加できる主要なチェックコード分析ルールセットを作成することによって、主要なガイドラインの取り組みをサポートしています。 パッケージは CppCoreCheck という名前で、 [https://www.nuget.org/packages/Microsoft.CppCoreCheck](https://www.nuget.org/packages/Microsoft.CppCoreCheck)で入手できます。 このパッケージには、少なくとも Visual Studio 2015 with Update 1 がインストールされている必要があります。  
  
 また、パッケージは、ヘッダーのみのガイドラインサポートライブラリ (GSL) である依存関係として別のパッケージをインストールします。 GSL は、 [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)で GitHub から入手することもできます。  
  
## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>コード分析C++のコアチェックガイドラインを有効にする  
 C++コアチェックコード分析ツールを有効にするには、Visual Studio 内で確認するC++各プロジェクトに CppCoreCheck NuGet パッケージをインストールします。  
  
#### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project"></a>CppCoreCheck パッケージをプロジェクトに追加するには  
  
1. **ソリューションエクスプローラー**で、右クリックして、パッケージを追加するソリューション内のプロジェクトのコンテキストメニューを開きます。 [ **Nuget**パッケージの管理] を選択して、 **nuget パッケージマネージャー**を開きます。  
  
2. **[NuGet パッケージマネージャー]** ウィンドウで、CppCoreCheck を検索します。  
  
    ![Nuget パッケージマネージャーウィンドウに CppCoreCheck パッケージが表示されます](../code-quality/media/cppcorecheck-nuget-window.PNG "CPPCoreCheck_Nuget_Window")  
  
3. CppCoreCheck パッケージを選択し、 **[インストール]** をクリックして、プロジェクトに規則を追加します。  
  
   NuGet パッケージは、プロジェクトに対してコード分析を有効にしたときに呼び出される追加の MSBuild. .targets ファイルをプロジェクトに追加します。 この .targets ファイルは、Visual C++ Studio コード分析ツールに追加の拡張機能としてコアチェック規則を追加します。  
  
   プロジェクトのコード分析を有効にするには、プロジェクトの **[プロパティページ]** ダイアログの **[コード分析]** セクションで **[ビルド時にコード分析を有効にする]** チェックボックスをオンにします。  
  
   ![コード分析の全般設定のプロパティページ](../code-quality/media/cppcorecheck-codeanalysis-general.png "CPPCoreCheck_CodeAnalysis_General")  
  
   コアC++チェック規則は、コード分析が有効になったときに実行される既定の規則セットの一部になります。 C++コアチェック規則は開発中なので、一部の規則はすべてのコードで使用できるように準備されていない場合がありますが、開発時には有益な場合があります。 これらのルールは試験段階としてリリースされます。 プロジェクトのプロパティで、リリース済みまたは試験的な規則を実行するかどうかを選択できます。  
  
   ![コード分析拡張機能の設定のプロパティページ](../code-quality/media/cppcorecheck-codeanalysis-extensions.png "CPPCoreCheck_CodeAnalysis_Extensions")  
  
   C++コアチェック規則セットを有効または無効にするには、プロジェクトの **[プロパティページ]** ダイアログを開きます。 **[構成プロパティ]** で、 **[コード分析]** 、 **[拡張機能]** の順に展開します。 **[コアチェック (リリース) をC++有効]** にする または **[ C++コアチェックを有効にする (試験段階)** ] の横にあるドロップダウンコントロールで、[**はい]** または **[いいえ]** を選択します。 **[OK]** または **[適用]** を選択して、変更を保存します。  
  
## <a name="check-types-bounds-and-lifetimes"></a>型、境界、および有効期間のチェック  
 コアC++チェックパッケージには、現在、[タイプセーフ](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-type)、[境界の安全性](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-bounds)、および[有効期間の安全性](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-lifetime)のプロファイルのチェッカーが含まれています。  
  
 ここでは、 C++主要なチェックルールで検出できる問題の種類の例を示します。  
  
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
  
 次の例では、 C++主要なチェックルールで検出できる警告のいくつかを示します。  
  
- C26494 は rule 型です。 5: 常にオブジェクトを初期化します。  
  
- C26485 はルールの境界です。 3: 配列からポインターへの減衰がありません。  
  
- C26481 は rule Bounds です。 1: ポインター演算は使用しないでください。 代わりに `span` を使用してください  
  
  このコードC++をコンパイルするときに、コアチェックのコード分析のルールセットがインストールされ、有効になっている場合、最初の2つの警告が出力されますが、3番目の警告は抑制されます。 コード例のビルド出力を次に示します。  
  
**1 >------ビルドを開始しました: プロジェクト: CoreCheckExample、構成: デバッグ Win32--**  
**----**  
**1 > CoreCheckExample .cpp**  
**1 > CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.exe**  
**1 > CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.pdb (完全な PDB)**  
**c:\users\username\documents\visual studio 2015 \ プロジェクト \ corecheckexample**  
**ckexample\corecheckexample.cpp (6): warning C26494: 変数 ' arr ' は uninitializ**  
**ed。常にオブジェクトを初期化します。(type .5: https://go.microsoft.com/fwlink/p/?Link**  
**ID = 620421)**  
**c:\users\username\documents\visual studio 2015 \ プロジェクト \ corecheckexample**  
**ckexample\corecheckexample.cpp (7): warning C26485: Expression ' arr ': 次に対する配列はありません**  
**ポインターの減衰。(境界 3: https://go.microsoft.com/fwlink/p/?LinkID=620415)**  
= = = = = = = = = **= ビルド: 1 成功、0失敗、0更新、0スキップ =** = = = = = = = = =コードC++をより適切に記述するための主要ガイドラインがあります。 ただし、ルールまたはプロファイルを適用できないインスタンスがある場合は、コード内で直接非表示にするのが簡単です。 `gsl::suppress` 属性を使用して、次C++のコードブロックの規則違反を検出および報告するようにコアチェックを維持することができます。 個々のステートメントをマークして、特定のルールを抑制することができます。 特定のルール番号を含めずに `[[gsl::suppress(bounds)]]` を記述して、境界プロファイル全体を抑制することもできます。  
  
## <a name="use-the-guideline-support-library"></a>ガイドラインサポートライブラリを使用する  
 また、CppCoreCheck NuGet パッケージでは、Microsoft によるガイドラインサポートライブラリ (GSL) の実装を含むパッケージもインストールされます。 GSL は、 [http://www.nuget.org/packages/Microsoft.Gsl](https://www.nuget.org/packages/Microsoft.Gsl)のスタンドアロン形式でも使用できます。 このライブラリは、主要なガイドラインに従う場合に便利です。 GSL には、エラーが発生しやすい構造を代替として置き換えることができる定義が含まれています。 たとえば、`T*, length` のパラメーターのペアを `span<T>` 型に置き換えることができます。 GSL はオープンソースであるため、ライブラリのソース、コメント、または投稿を確認する場合は、 [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)にあるプロジェクトを参照してください。
