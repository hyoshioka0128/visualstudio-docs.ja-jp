---
title: VSIX パッケージの解剖学 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a6d3f994c531bd36ab4281c5f0b27e993cd3392
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740095"
---
# <a name="anatomy-of-a-vsix-package"></a>VSIX パッケージの解剖学
VSIX パッケージは、1 つまたは複数の Visual Studio 拡張機能を含む *.vsix*ファイルです。 そのメタデータは、VSIX マニフェストと *[Content_Types].xml*ファイルに含まれています。 VSIX パッケージには、ローカライズされたセットアップ テキストを提供する 1 つ以上*の Extension.vsixlangpack*ファイルが含まれている場合があり、依存関係をインストールするための追加の VSIX パッケージが含まれている場合があります。

 VSIX パッケージ形式は、オープン パッケージ規則 (OPC) 標準に従います。 パッケージには、バイナリファイルとサポートファイルが含まれ *、[Content_Types].xml*ファイルと *.vsix*マニフェストファイルが含まれています。 1 つの VSIX パッケージには、複数のプロジェクトの出力が含まれている場合があります。

> [!NOTE]
> VSIX パッケージに含まれるファイルの名前には[\[、RFC2396\]](https://www.rfc-editor.org/rfc/rfc2396.txt)で定義されているスペースや、統一リソース識別子 (URI) に予約されている文字を含めることはできません。

## <a name="the-vsix-manifest"></a>VSIX マニフェスト
 VSIX マニフェストには、インストールする拡張機能に関する情報が含まれ、VSX スキーマに従います。 詳細については[、VSIX 拡張スキーマ 1.0 リファレンス](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)を参照してください。 VSIX マニフェストの例については、「[パッケージ マニフェスト要素 (ルート要素、VSX スキーマ)」](https://msdn.microsoft.com/library/f8ae42ba-775a-4d2b-976a-f556e147f187)を参照してください。

 VSIX マニフェストは、^.vsix* ファイルに含まれている場合に名前を付`extension.vsixmanifest`ける必要があります。

## <a name="the-content"></a>内容
 VSIX パッケージには、テンプレート、ツールボックス項目、VSPackages、または Visual Studio でサポートされているその他の種類の拡張機能を含めることができます。

## <a name="language-packs"></a>言語パック
 VSIX パッケージには、インストール時にローカライズされたテキストを提供する 1 つ以上*の Extension.vsixlangpack*ファイルが含まれる場合があります。 詳しくは[、VSIX パッケージのローカライズを](../extensibility/localizing-vsix-packages.md)参照してください。

## <a name="dependencies-and-references"></a>依存関係と参照
 VSIX パッケージには、参照として他の VSIX パッケージを含めることができます。 これらの他のパッケージには、それぞれ独自の VSIX マニフェストが含まれている必要があります。

 ユーザーが依存関係を持つ拡張機能をインストールしようとすると、インストーラーは、必要なアセンブリがユーザー システムにインストールされていることを確認します。 必要なアセンブリが見つからない場合、**拡張機能と更新プログラム**は、不足しているアセンブリの一覧を表示します。

 拡張機能マニフェストに 1 つ以上の[Reference](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100))要素が含まれている場合、**拡張機能と更新プログラム**は、各参照のマニフェストをシステムにインストールされている拡張機能と比較し、まだインストールされていない場合は、参照される拡張機能をインストールします。 参照されている拡張機能の以前のバージョンがインストールされている場合は、新しいバージョンで置き換えられます。

 複数プロジェクトのソリューション内のプロジェクトに、同じソリューション内の別のプロジェクトへの参照が含まれている場合、VSIX パッケージには、そのプロジェクトの依存関係が含まれます。 この動作をオーバーライドするには、内部プロジェクトの参照をクリックし、[**プロパティ]** ウィンドウで **[VSIX に含まれる出力グループ**] プロパティ`BuiltProjectOutputGroup`を に設定します。

 参照アセンブリのサテライト DLL を VSIX パッケージに含`SatelliteDllsProjectOutputGroup`めるには **、VSIX プロパティに含まれる出力グループを**追加します。

## <a name="installation-location"></a>インストール場所
 インストール中に、**拡張機能と更新プログラム**は *、%LocalAppData%\Microsoft\VisualStudio\14.0\拡張機能*の下のフォルダー内の VSIX パッケージの内容を検索します。

 *%LocalAppData%* はユーザー固有のディレクトリであるため、デフォルトでは、現在のユーザーにのみインストールが適用されます。 ただし、マニフェストの[AllUsers](https://msdn.microsoft.com/library/ac817f50-3276-4ddb-b467-8bbb1432455b)要素を`True`に設定すると、拡張機能は<em>.\\</em>コンピュータのすべてのユーザーが<em>\Common7\IDE\Extensions</em>使用できるようになります。

## <a name="content_typesxml"></a>[Content_Types].xml
 *[Content_Types].xml*ファイルは、展開された *.vsix*ファイル内のファイルの種類を識別します。 Visual Studio では、パッケージのインストール時にこのファイルが使用されますが、ファイル自体はインストールされません。 このファイルの詳細については[、「Content_types].xml ファイルの構造](the-structure-of-the-content-types-dot-xml-file.md)」を参照してください。

 *[Content_Types].xml*ファイルは、オープン パッケージ規則 (OPC) 標準で必要です。 OPC の詳細については、「OPC: MSDN Web サイトで[データをパッケージ化するための新しい標準](https://blogs.msdn.microsoft.com/msdnmagazine/2007/08/08/opc-a-new-standard-for-packaging-your-data/)」を参照してください。
