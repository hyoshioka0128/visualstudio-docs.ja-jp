---
title: VSCT コンパイラのコマンドラインフラグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98cd0ec51ead200a904baeb409551cd1084f1f11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842033"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT コンパイラのコマンドライン フラグ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio コマンドテーブル (VSCT) コンパイラには、vsct ファイルのコンパイルが正常に行われるようにするためのコマンドラインスイッチが用意されています。  
  
## <a name="command-line-parameters"></a>コマンドラインパラメーター  
 コマンドウィンドウから基本的な VSCT ヘルプを表示するには、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** *Visual Studio SDK のインストールパス*\VisualStudioIntegration\Tools\Bin\ フォルダーに移動し、次のように入力します。  
  
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
> 文字-(ダッシュ) と/(スラッシュ) はどちらも、コマンドラインパラメーターを示すために使用できます。  
  
 使用可能なフラグとその意味は次のとおりです。  
  
|Switch|説明|  
|------------|-----------------|  
|-d|定義されている追加のシンボルを指定します。|  
|-I|ファイル参照を解決するときに使用する追加のインクルードパスを指定します。|  
|-l|カルチャ名を指定し <xref:System.Globalization.CultureInfo> ます (例: "en-us")。|  
|-E|コマンド項目に対して指定した名前空間の C# オブジェクトを出力し、その後に [C&#124;H&#124;N]:*filename*を生成します。 c = C#、H = C++ ヘッダー、N = 名前空間。 C# では名前空間が必要です。|  
|-v|詳細出力。|  
  
 -L スイッチは、文字列のグループを選択して、指定されたカルチャ名に対応するバイナリの cto ファイルを生成するようにコンパイラに指示します。 <xref:System.Globalization.CultureInfo> 指定されたカルチャ名は、vsct ファイル内の1つ以上の [文字列要素](../../extensibility/strings-element.md) の言語属性と一致する必要があります。 Strings 要素に言語属性がない場合は、それを含んでいる [Commandtable 要素](../../extensibility/commandtable-element.md)から継承されます。  
  
 Vsct ファイルには、複数の文字列要素を含めることができ、それぞれの言語属性が異なる場合があります。 グローバリゼーションは、VSCT コンパイラを複数回実行し、各カルチャ名の-L スイッチを変更することで実現されます。  
  
 -L スイッチによって指定されたカルチャ名が文字列要素の Language 属性と一致しない場合、コンパイラは地域ではなく、言語との照合を試みます。 たとえば、"en-us" が見つからない場合、コンパイラは代わりに "en" を試行します。 失敗した場合、オペレーティングシステムの現在のカルチャが試行されます。 失敗した場合は、最初に見つかった文字列要素がコンパイルされます。  
  
 -E スイッチを使用すると、コマンドテーブルによって使用されるシンボルを含む C スタイルのヘッダーファイルを出力したり、コマンドシンボルのオブジェクトを含む C# ファイルを生成したりできます。  
  
 -D および– I スイッチには、同じ名前を持つ Cl.exe C プリプロセッサフラグの構文があります。 X = Y という形式の– D 定義は、属性で XML ベースのテストを展開するために使用され \<Defined> `Condition` ます。 – I パスは \<Include> 、およびファイル参照を解決するために使用され \<Extern> \<Bitmap> ます。 詳細については、「 [Vsct XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)」を参照してください。  
  
 VSCT コンパイラは、以前にビルドされたバイナリファイルを逆コンパイルすることもできます。 これを行うには、のバイナリファイルを指定し \<infile> ます。   バイナリファイルが VSCT コンパイラによって生成された場合、そのシンボルは既に埋め込まれており、出力のセクションにシンボリック名を含む出力が生成され \<Symbols> ます。 バイナリが CTC コンパイラによって生成された場合、出力には実際の Guid と Id が含まれます。 現在のバージョンの Ctc.exe によって生成された * ctsym ファイルがバイナリ入力ファイルと同じフォルダーにある場合、シンボルはそのファイルから読み込まれ、出力に使用されます。  
  
## <a name="see-also"></a>参照  
 [Visual Studio コマンドテーブル (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [VSCT XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)   
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
