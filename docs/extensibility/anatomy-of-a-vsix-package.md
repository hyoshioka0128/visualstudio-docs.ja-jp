---
title: VSIX パッケージの構造 |Microsoft Docs
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
ms.openlocfilehash: c52f87426b9f06ad40d77c2cc9e7be1627d2c82d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88250820"
---
# <a name="anatomy-of-a-vsix-package"></a>VSIX パッケージの構造
VSIX パッケージは、1つまたは複数の Visual Studio 拡張機能を含む *.vsix* ファイルで、visual studio が拡張機能を分類およびインストールするために使用するメタデータと共に使用されます。 このメタデータは、VSIX マニフェストと *[Content_Types] .xml* ファイルに格納されています。 VSIX パッケージには、ローカライズされたセットアップテキストを提供するための *vsixlangpack* ファイルが1つ以上含まれている場合があります。また、依存関係をインストールするための vsix パッケージが追加されている場合もあります。

 VSIX パッケージ形式は、Open パッケージング規約 (OPC) 標準に従います。 パッケージには、バイナリおよびサポートファイルと共に、 *[Content_Types] .xml* ファイルと *.vsix* マニフェストファイルが含まれています。 1つの VSIX パッケージに、複数のプロジェクトの出力、または独自のマニフェストを持つ複数のパッケージが含まれている場合があります。

> [!NOTE]
> VSIX パッケージに含まれるファイルの名前には、 [ \[ RFC2396 \] ](https://www.rfc-editor.org/rfc/rfc2396.txt)で定義されているように、スペースや、UNIFORM resource identifier (URI) で予約されている文字を含めることはできません。

## <a name="the-vsix-manifest"></a>VSIX マニフェスト
 VSIX マニフェストには、インストールする拡張機能に関する情報が含まれており、VSX スキーマに従います。 詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)」を参照してください。 VSIX マニフェストの例については、「 [PackageManifest 要素 (root 要素、VSX schema)](https://msdn.microsoft.com/library/f8ae42ba-775a-4d2b-976a-f556e147f187)」を参照してください。

 VSIX マニフェストは、 `extension.vsixmanifest` ^ .vsix * ファイルに含まれている場合は、という名前にする必要があります。

## <a name="the-content"></a>コンテンツ
 VSIX パッケージには、テンプレート、ツールボックスアイテム、Vspackage、または Visual Studio でサポートされているその他の種類の拡張機能が含まれている場合があります。

## <a name="language-packs"></a>言語パック
 VSIX パッケージには、インストール時にローカライズされたテキストを提供するための *vsixlangpack* ファイルが1つ以上含まれている場合があります。 詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="dependencies-and-references"></a>依存関係と参照
 VSIX パッケージには、参照として他の VSIX パッケージを含めることができます。 これらの他のパッケージにはそれぞれ、独自の VSIX マニフェストが含まれている必要があります。

 依存関係がある拡張機能をユーザーがインストールしようとすると、インストーラーは必要なアセンブリがユーザーシステムにインストールされていることを確認します。 必要なアセンブリが見つからない場合は、 **拡張機能と更新プログラム** によって、不足しているアセンブリの一覧が表示されます。

 拡張機能マニフェストに1つ以上の [参照](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100)) 要素が含まれている場合、 **拡張機能と更新プログラム** は、各参照のマニフェストをシステムにインストールされている拡張機能と比較し、まだインストールされていない場合は、参照される拡張機能をインストールします。 以前のバージョンの参照されている拡張機能がインストールされている場合は、新しいバージョンで置き換えられます。

 複数プロジェクトのソリューション内のプロジェクトに、同じソリューション内の別のプロジェクトへの参照が含まれている場合、VSIX パッケージにはそのプロジェクトの依存関係が含まれます。 この動作をオーバーライドするには、内部プロジェクトの参照を選択し、[ **プロパティ** ] ウィンドウで、VSIX プロパティ **に含まれる出力グループ** をに設定し `BuiltProjectOutputGroup` ます。

 参照されたアセンブリのサテライト Dll を VSIX パッケージに含めるには、 `SatelliteDllsProjectOutputGroup` **vsix プロパティに含まれる出力グループ** にを追加します。

## <a name="installation-location"></a>インストール場所
 インストール中、 **拡張機能と更新プログラム** によって、 *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions*の下のフォルダーにある VSIX パッケージの内容が検索されます。

 既定では、 *% Localappdata%* はユーザー固有のディレクトリであるため、インストールは現在のユーザーにのみ適用されます。 ただし、マニフェストの[AllUsers](https://msdn.microsoft.com/library/ac817f50-3276-4ddb-b467-8bbb1432455b)要素をに設定すると、 `True` 拡張機能がにインストール<em> \\ されます。</em>VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em>とは、コンピューターのすべてのユーザーが使用できるようになります。

## <a name="content_typesxml"></a>[Content_Types] .xml
 *[Content_Types] .xml*ファイルは、展開された *.vsix*ファイル内のファイルの種類を識別します。 Visual Studio では、パッケージのインストール時にこのファイルを使用しますが、ファイル自体はインストールしません。 このファイルの詳細については、 [[Content_types] .xml ファイルの構造](the-structure-of-the-content-types-dot-xml-file.md)を参照してください。

 Open パッケージング規約 (OPC) 標準では、 *[Content_Types] .xml* ファイルが必要です。 OPC の詳細については、「 [opc: データをパッケージ化するための新しい標準](https://blogs.msdn.microsoft.com/msdnmagazine/2007/08/08/opc-a-new-standard-for-packaging-your-data/) 」を参照してください。
