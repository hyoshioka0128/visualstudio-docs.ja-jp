---
title: TextTransform ユーティリティを使用したファイルの生成
ms.date: 07/26/2019
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ec659bfee9253dfb198c2747e1b5d7fb6b78f2b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596555"
---
# <a name="generate-files-with-the-texttransform-utility"></a>TextTransform ユーティリティを使用したファイルの生成

TextTransform.exe は、テキスト テンプレートを変換するために使用できるコマンド ライン ツールです。 TextTransform.exe を呼び出すときに、引数として、テキスト テンプレート ファイルの名前を指定します。 TextTransform.exe では、テキスト変換エンジンを呼び出し、テキスト テンプレートを処理します。 TextTransform.exe は通常、スクリプトから呼び出されます。 ただし、Visual Studio あるいは、ビルド プロセスの中で、テキスト変換が実行されるため、通常、必須ではありません。

> [!NOTE]
> ビルド プロセスの一部としてテキスト変換を実行する場合は、MSBuild のテキスト変換タスクの使用を検討してください。 詳細については、「[ビルド プロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。 Visual Studio がインストールされているコンピューターでは、テキスト テンプレートを変換するアプリケーションあるいは Visual Studio 拡張機能を作成することもできます。 詳細については、「[カスタム ホストを使用してテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)」をご覧ください。

TextTransform.exe は、次のディレクトリにあります。

::: moniker range=">=vs-2019"

**ファイル (x86) \Microsoft Visual Studio\2019\Professional\Common7\IDE**

Professional edition の場合は、または

**ファイル (x86) \Microsoft Visual Studio\2019\Enterprise\Common7\IDE**

Enterprise edition の場合。

::: moniker-end

::: moniker range="vs-2017"

Professional edition:

Professional edition の場合は、または

Enterprise edition:

Enterprise edition の場合。

Visual Studio の以前のバージョンでは、次の場所にファイルがあります。

**\Program Files (x86)\Common Files\Microsoft Shared\TextTemplating\{version}**

{version} は、インストールされている Visual Studio のバージョンによります。

::: moniker-end

## <a name="syntax"></a>構文

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>パラメーター

|**引数**|**説明**|
|-|-|
|`templateName`|変換するテンプレート ファイルの名前を示します。|

|**オプション**|**説明**|
|-|-|
|**-out** \<filename>|変換の出力を書き込むファイル。|
|**-r** \<assembly>|テキスト テンプレートをコンパイルし実行するために使用するアセンブリ。|
|**-u** \<namespace>|テンプレートのコンパイルに使用される名前空間。|
|**-I** \<includedirectory>|テキスト テンプレートでインクルードすることが指定されたテキスト テンプレートが含まれるディレクトリ。|
|**-P** \<referencepath>|テキスト テンプレート内、あるいは、 **-r** オプションで指定されたアセンブリを検索するディレクトリ。<br /><br /> たとえば、Visual Studio API を使用するアセンブリを含めるためには次のようにします。<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|テキスト テンプレートの中でカスタム ディレクティブの処理に使用できるディレクティブ プロセッサの名前、完全な型の名前、および、アセンブリ。|
|**-** [processorName] [。directiveName]。\<parameterName >!\<parameterValue >|ディレクティブ プロセッサのパラメーター値を指定します。 パラメーター名と値のみを指定したパラメーターはすべてのディレクティブ プロセッサで利用できます。 ディレクティブ プロセッサを指定した場合、パラメーターが指定したプロセッサのみが使用できます。 ディレクティブの名前を指定する場合、パラメーターの値は、指定されたディレクティブが処理されている場合にのみ使用です。<br /><br /> ディレクティブ プロセッサまたはテキスト テンプレートからパラメーター値にアクセスするには、[ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))を使用します。 テキスト テンプレート中に、`hostspecific` template ディレクティブを含め、`this.Host` 上のメッセージを呼び出します。 例:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> 入力省略可能なプロセッサとディレクティブの名前を省略した場合でも、'!'マークは常にタイプします。 例:<br /><br /> `-a !!param!value`|
|**-h**|ヘルプを提供します。|

## <a name="related-topics"></a>関連トピック

|タスク|トピック|
|-|-|
|Visual Studio ソリューション中での ファイル の生成。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|
|独自のアプリケーションからテキスト テンプレートを呼び出すことができるテキスト テンプレート ホストの作成。|[カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)|
