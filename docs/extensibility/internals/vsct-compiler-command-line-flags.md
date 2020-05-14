---
title: VSCT コンパイラのコマンド ライン フラグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e4ee29710049453c3163c366eccf96e257b6028d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703968"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT コンパイラのコマンドライン フラグ
Visual Studio コマンド テーブル (VSCT) コンパイラには、.vsct ファイルのコンパイルを成功させるためにコマンド ライン スイッチが用意されています。

## <a name="command-line-parameters"></a>コマンド ライン パラメータ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**コマンド**ウィンドウから基本的な VSCT ヘルプを表示するには *、Visual Studio SDK のインストール パス*\VisualStudioIntegration\ツール\Bin\ フォルダーに移動し、次のように入力します。

```
vsct /?
```

 次が返されます。

```
Microsoft (R) Visual Studio (R) Command Table Compiler Version 3.00.2000

Syntax: vsct <infile> [<outfile>] [-S[symbols file]] [-D<preprocessor-define>]*
[-I<include-path>]* [-L<language>] [-E[C|H|N]:<name>]

  -D    Specify any additional preprocessor defines
  -I    Indicate what additional include paths to send to the preprocessor
  -L    Specify the language to use when selecting strings
  -E    Emit C# objects in the specified namespace for command items,
        followed by [L|F|H|N]:<value>
        F = Name of the file to emit (used if -EL is provided)
        L = Name of a language providing a CodeDOM provider
        N = namespace (required if -EL is provided)
        H = C++ header
  -c    Clean build skipping dependency checks
  -v    Verbose output
```

> [!NOTE]
> 文字 - (ダッシュ) と / (スラッシュ) は、両方ともコマンド 行パラメーターを示す表記を受け入れます。

 許容可能なフラグとそれらが意味するものは次のとおりです。

|Switch|説明|
|------------|-----------------|
|-d|追加の定義済みシンボルを指定します。|
|-I|ファイル参照を解決するときに使用する追加のインクルード パスを指定します。|
|-l|カルチャ名<xref:System.Globalization.CultureInfo>を指定します ("en-US" など)。|
|-E|コマンド項目の指定された名前空間で C# オブジェクトを出力し、[C&#124;H&#124;N]:*ファイル名 C*= C#、H = C = ヘッダー、N = 名前空間。 C# には名前空間が必要です。|
|-v|詳細出力。|

 L スイッチは、指定<xref:System.Globalization.CultureInfo>されたカルチャ名に対応するバイナリ .cto ファイルを生成する文字列のグループを選択するようにコンパイラに指示します。 指定したカルチャ名は、.vsct ファイル内の 1 つ以上の[Strings 要素](../../extensibility/strings-element.md)の言語属性と一致する必要があります。 文字列要素に言語属性がない場合は、それを含む[CommandTable 要素](../../extensibility/commandtable-element.md)から継承されます。

 vsct ファイルには複数の文字列要素があり、それぞれ異なる言語属性を持つ場合があります。 グローバリゼーションは、VSCT コンパイラを複数回実行し、カルチャ名ごとに -L スイッチを変更することで実現されます。

 -L スイッチによって指定されたカルチャ名が Strings 要素の言語属性と一致しない場合、コンパイラは、地域ではなく言語と一致しようとします。 たとえば、"en-US" が見つからない場合、コンパイラは代わりに "en" を試みます。 失敗すると、オペレーティング システムの現在のカルチャが試されます。 失敗すると、最初に見つかった Strings 要素がコンパイルされます。

 -E スイッチを使用すると、コマンド テーブルで使用されるシンボルを含む C スタイルのヘッダー ファイルを出力したり、コマンド シンボルのオブジェクトを含む C# ファイルを出力したりできます。

 -D スイッチと -I スイッチには、同じ名前を持つ Cl.exe C プリプロセッサ フラグの構文があります。 形式 X=Y の -D 定義は、属性の XML\<ベースの定義>`Condition`テストの拡張に使用されます。 -I インクルード>、Extern>、\<\<ビットマップ>ファイル参照\<を解決するためにパスを使用しています。 詳細については、「 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)」を参照してください。

 VSCT コンパイラは、以前にビルドされたバイナリ ファイルを逆コンパイルすることもできます。 これを行うには、infile>のバイナリ\<ファイルを指定します。   バイナリ ファイルが VSCT コンパイラによって生成された場合、そのバイナリ ファイルには既にシンボルが埋め込まれ、\<シンボル名が出力のシンボル> セクションに出力されます。 バイナリが CTC コンパイラによって生成された場合、出力には実際の GUID と ID が含まれます。 現在のバージョンの Ctc.exe によって生成された *.ctsym ファイルがバイナリ入力ファイルと同じフォルダーにある場合、シンボルはそのファイルから読み込まれ、出力に使用されます。

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
