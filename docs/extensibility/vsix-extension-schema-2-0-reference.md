---
title: VSIX 拡張スキーマ 2.0 リファレンス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78e260c62d67afc10fea25d52169c48b64c82f72
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697921"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 拡張スキーマ 2.0 リファレンス
VSIX 配置マニフェスト ファイルは、VSIX パッケージの内容を記述します。 ファイル形式はスキーマによって制御されます。 このスキーマのバージョン 2.0 では、カスタム型と属性の追加がサポートされています。  マニフェストのスキーマは拡張可能です。 マニフェスト ローダーは、理解できない XML 要素と属性を無視します。

> [!IMPORTANT]
> Visual Studio 2015 は、VSIX ファイルを読み込むことができます。

## <a name="package-manifest-schema"></a>パッケージ マニフェスト スキーマ
 マニフェスト XML ファイルのルート要素は`<PackageManifest>`です。 マニフェスト形式のバージョンである`Version`単一の属性があります。 フォーマットに大きな変更が加えられた場合、バージョンの形式が変更されます。 この資料では、バージョン 2.0 の`Version`属性を Version="2.0" の値に設定することでマニフェスト形式のバージョン 2.0 について説明します。

### <a name="packagemanifest-element"></a>パッケージマニフェスト要素
 ルート要素`<PackageManifest>`内では、次の要素を使用できます。

- `<Metadata>`- パッケージ自体に関するメタデータと広告情報。 マニフェストで`Metadata`使用できる要素は 1 つだけです。

- `<Installation>`- このセクションでは、この拡張パッケージをインストールするアプリケーション SKU を含む、この拡張パッケージをインストールする方法を定義します。 マニフェストでは、1 つの`Installation`要素のみを使用できます。 マニフェストには要素が`Installation`必要です。

- `<Dependencies>`- このパッケージの依存関係のオプションの一覧は、ここで定義されています。

- `<Assets>`- このセクションには、このパッケージに含まれるすべてのアセットが含まれています。 このセクションがないと、このパッケージはコンテンツを表示しません。

- `<AnyElement>*`- マニフェスト スキーマは、他の要素を許可するのに十分な柔軟性があります。 マニフェスト ローダーで認識されない子要素は、拡張機能マネージャー API で追加の XmlElement オブジェクトとして公開されます。 これらの子要素を使用して、VSIX 拡張機能は、Visual Studio で実行されているコードが実行時にアクセスできるマニフェスト ファイル内の追加データを定義できます。 [「追加要素](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))」を参照してください。

### <a name="metadata-element"></a>メタデータ要素
 このセクションは、パッケージ、ID、および広告情報に関するメタデータです。 `<Metadata>`には、次の要素が含まれます。

- `<Identity>`- このパッケージの識別情報を定義し、次の属性を含めます。

  - `Id`- この属性は、作成者が選択したパッケージの一意の ID である必要があります。 名前は、CLR 型が名前空間に格納されているのと同じ方法で修飾する必要 Company.Product.Feature.Nameがあります。 属性`Id`は 100 文字に制限されています。

  - `Version`- このパッケージのバージョンとその内容を定義します。 この属性は、CLR アセンブリのバージョン管理形式に従います。 より高いバージョン番号を持つパッケージは、パッケージの更新と見なされ、既存のインストール済みバージョンにインストールできます。

  - `Language`- この属性はパッケージの既定の言語であり、このマニフェストのテキスト データに対応します。 この属性は、リソース アセンブリの CLR ロケール コード規則に従います。 任意のバージョン`neutral`の Visual Studio で実行される言語に依存しない拡張機能を宣言するように指定できます。 既定値は `neutral` です。

  - `Publisher`- この属性は、このパッケージの発行者 (会社名または個人名) を識別します。 属性`Publisher`は 100 文字に制限されています。

- `<DisplayName>`- この要素は、拡張機能マネージャー UI に表示されるわかりやすいパッケージ名を指定します。 コンテンツ`DisplayName`は 50 文字に制限されています。

- `<Description>`- このオプションの要素は、パッケージとその内容の簡単な説明で、拡張機能マネージャー UI に表示されます。 コンテンツ`Description`には、必要な任意のテキストを含めることができますが、1000 文字に制限されています。

- `<MoreInfo>`- このオプション要素は、このパッケージの完全な説明を含むオンライン ページへの URL です。 プロトコルは http として指定する必要があります。

- `<License>`- このオプションの要素は、パッケージに含まれるライセンス ファイル (.txt、.rtf) への相対パスです。

- `<ReleaseNotes>`- このオプション要素は、パッケージ (.txt、.rtf) に含まれるリリース ノート ファイルへの相対パス、またはリリース ノートを表示する Web サイトへの URL のいずれかです。

- `<Icon>`- このオプション要素は、パッケージに含まれるイメージファイル(png、bmp、jpeg、ico)への相対パスです。 アイコン イメージは 32 x 32 ピクセル (または、そのサイズに縮小されます) にする必要があり、リストビュー UI に表示されます。 要素が`Icon`指定されていない場合、UI は既定値を使用します。

- `<PreviewImage>`- このオプションの要素は、パッケージに含まれるイメージ ファイル (png、bmp、jpeg) への相対パスです。 プレビュー イメージは 200 x 200 ピクセルで、詳細 UI に表示されます。 要素が`PreviewImage`指定されていない場合、UI は既定値を使用します。

- `<Tags>`- このオプションの要素は、検索ヒントに使用される追加のセミコロン区切りのテキスト タグを一覧表示します。 要素`Tags`は 100 文字に制限されています。

- `<GettingStartedGuide>`- このオプションの要素は、HTML ファイルへの相対パスか、このパッケージ内の拡張機能またはコンテンツの使用方法に関する情報を含む Web サイトの URL です。 このガイドは、インストールの一部として起動されます。

- `<AnyElement>*`- マニフェスト スキーマは、他の要素を許可するのに十分な柔軟性があります。 マニフェスト ローダーで認識されない子要素は、XmlElement オブジェクトのリストとして公開されます。 これらの子要素を使用すると、VSIX 拡張機能を使用して、マニフェスト ファイルに追加のデータを定義し、実行時に列挙できます。

### <a name="installation-element"></a>インストール要素
 このセクションでは、このパッケージをインストールする方法と、インストール先のアプリケーション SKU を定義します。 このセクションには、次の属性が含まれています。

- `Experimental`- すべてのユーザーに現在インストールされている拡張機能があるが、同じコンピューター上で更新バージョンを開発している場合は、この属性を true に設定します。 たとえば、すべてのユーザーに MyExtension 1.0 をインストールし、同じコンピューターで MyExtension 2.0 をデバッグする場合は、実験="true" を設定します。 この属性は、Visual Studio 2015 更新プログラム 1 以降で使用できます。

- `Scope`- この属性は、値 "グローバル" または "製品拡張" を受け取ることができます。

  - "Global" は、インストールのスコープが特定の SKU に限定されないことを指定します。 たとえば、この値は、拡張 SDK がインストールされている場合に使用されます。

  - "ProductExtension" は、個々の Visual Studio SKU を対象とする従来の VSIX 拡張 (バージョン 1.0) がインストールされることを指定します。 これが既定値です。

- `AllUsers`- このオプション属性は、このパッケージをすべてのユーザーにインストールするかどうかを指定します。 既定では、この属性は false で、パッケージがユーザーごとに指定されます。 (この値を true に設定すると、インストールユーザーは、結果として生じる VSIX をインストールするために、管理特権レベルに昇格する必要があります。

- `InstalledByMsi`- このオプション属性は、このパッケージが MSI によってインストールされるかどうかを指定します。 MSI によってインストールされたパッケージは、Visual Studio 拡張機能マネージャーではなく、MSI (プログラムと機能) によってインストールおよび管理されます。  既定では、この属性は false で、パッケージが MSI によってインストールされないことを指定します。

- `SystemComponent`- このオプション属性は、このパッケージをシステム コンポーネントと見なすかどうかを指定します。 システム コンポーネントは、拡張機能マネージャーの UI に表示されず、更新できません。 既定では、この属性は false で、パッケージがシステム コンポーネントではないことを指定します。

- `AnyAttribute*`-`Installation`要素は、実行時に名前と値のペアのディクショナリとして公開される属性のオープン エンドのセットを受け入れます。

- `<InstallationTarget>`-この要素は、VSIX インストーラーがパッケージをインストールする場所を制御します。 `Scope`属性の値が "ProductExtension" の場合、パッケージは、そのコンテンツの一部としてマニフェスト ファイルをインストールして、その可用性を拡張機能に通知する SKU を対象にする必要があります。 属性が明示的または既定値の "ProductExtension" を持つ場合、要素には`<InstallationTarget>`次の属性があります。 `Scope`

  - `Id`- この属性はパッケージを識別します。  属性は、名前空間の規則に従ってCompany.Product.Feature.Name。 属性`Id`には英数字のみを含めることができ、100 文字に制限されます。 期待値:

    - 統合シェル

    - Microsoft.VisualStudio.Pro

    - プレミアム

    - 究極の

    - マイクロソフトは、ビジュアルスタジオ.VWDエクスプレス

    - をクリックします。

    - を使用します。

    - を使用します。

    - 私のシェル.アプリ

  - `Version`- この属性は、この SKU のサポートされる最小バージョンと最大バージョンを持つバージョン範囲を指定します。 パッケージは、サポートする SKU のバージョンを詳述できます。 バージョン範囲の表記は[10.0 - 11.0]です。

    - [ - 最小バージョンを含む。

    - ] - 最大バージョンを含む。

    - ( - 最小バージョン限定。

    - ) - 最大バージョン限定。

    - 単一バージョン # - 指定されたバージョンのみ。

    > [!IMPORTANT]
    > VSIX スキーマのバージョン 2.0 は、Visual Studio 2012 で導入されました。 このスキーマを使用するには、コンピューターに Visual Studio 2012 以降をインストールし、その製品の一部である VSIXInstaller.exe を使用する必要があります。 Visual Studio 2012 以降の VSIX インストーラーを使用して、以前のバージョンの Visual Studio を対象とできますが、インストーラーの新しいバージョンを使用する必要があります。

    Visual Studio 2017 のバージョン番号は[、Visual Studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md)で見つけることができます。

    Visual Studio 2017 リリースのバージョンを表現する場合、マイナー バージョンは常に**0**にする必要があります。 たとえば、Visual Studio 2017 バージョン 15.3.26730.0 は [15.0.26730.0,16.0] と表現する必要があります。 これは、Visual Studio 2017 以降のバージョン番号でのみ必要です。

  - `AnyAttribute*`-`<InstallationTarget>`この要素は、実行時に名前と値のペアディクショナリとして公開される、オープンエンドの属性セットを許可します。

### <a name="dependencies-element"></a>依存関係要素
 この要素には、このパッケージが宣言する依存関係の一覧が含まれています。 依存関係が指定されている場合は、それらのパッケージ (`Id`で識別される ) が以前にインストールされている必要があります。

- `<Dependency>`要素 - この子要素には、次の属性があります。

  - `Id`- この属性は、依存パッケージの一意の ID である必要があります。 この ID 値は`<Metadata><Identity>Id`、このパッケージが依存するパッケージの属性と一致する必要があります。 属性`Id`は、名前空間の規則に従ってCompany.Product.Feature.Name。 属性には英数字のみを含めることができ、100 文字に制限されます。

  - `Version`- この属性は、この SKU のサポートされる最小バージョンと最大バージョンを持つバージョン範囲を指定します。 パッケージは、サポートする SKU のバージョンを詳述できます。 バージョン範囲の表記は [12.0, 13.0] で、次の場合があります。

    - [ - 最小バージョンを含む。

    - ] - 最大バージョンを含む。

    - ( - 最小バージョン限定。

    - ) - 最大バージョン限定。

    - 単一バージョン # - 指定されたバージョンのみ。

  - `DisplayName`- この属性は、ダイアログ ボックスやエラー メッセージなどの UI 要素で使用される依存パッケージの表示名です。 依存パッケージが MSI によってインストールされていない限り、この属性はオプションです。

  - `Location`- この省略可能な属性は、ネストされた VSIX パッケージへのこの VSIX 内の相対パス、または依存関係のダウンロード場所への URL を指定します。 この属性は、ユーザーが前提条件パッケージを見つけやすくするために使用されます。

  - `AnyAttribute*`-`Dependency`要素は、実行時に名前と値のペアのディクショナリとして公開される属性のオープン エンドのセットを受け入れます。

### <a name="assets-element"></a>資産要素
 この要素には、このパッケージ`<Asset>`によって表示される各拡張要素またはコンテンツ要素のタグのリストが含まれます。

- `<Asset>`- この要素には、次の属性と要素が含まれています。

  - `Type`- この要素で表される拡張機能またはコンテンツの種類。 各`<Asset>`要素は 1`Type`つの 要素`<Asset>`を持つ必要がありますが`Type`、複数の要素が同じ である場合があります。 この属性は、名前空間の規則に従って完全修飾名として表す必要があります。 既知の型は次のとおりです。

    1. を使用します。

    2. Microsoft.VisualStudio.MefComponent

    3. ツールボックスコントロール

    4. サンプル

    5. テンプレート

    6. 項目テンプレート

    7. アセンブリ

       独自の型を作成し、一意の名前を付けることができます。 Visual Studio 内の実行時に、コードは拡張機能マネージャー API を使用してこれらのカスタム型を列挙してアクセスできます。

  - `Path`- アセットを含むパッケージ内のファイルまたはフォルダへの相対パス。

  - `TargetVersion`- 指定された資産が適用されるバージョン範囲。 複数のバージョンのアセットを異なるバージョンの Visual Studio に配布するために使用されます。 効果を持つには、Visual Studio 2017.3 以降が必要です。

  - `AnyAttribute*`- 実行時に名前と値のペアのディクショナリとして公開される、オープン エンドの属性のセット。

    `<AnyElement>*`- 開始タグと終了タグの`<Asset>`間に、構造化されたコンテンツを使用できます。 すべての要素は、XmlElement オブジェクトのリストとして公開されます。 VSIX 拡張機能では、マニフェスト ファイルに構造化された型固有のメタデータを定義し、実行時に列挙できます。

### <a name="sample-manifest"></a>サンプル マニフェスト

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
  <Metadata>
    <Identity Id="0000000-0000-0000-0000-000000000000" Version="1.0" Language="en-US" Publisher="Company" />
    <DisplayName>Test Package</DisplayName>
    <Description>Information about my package</Description>
    <MoreInfo>http://www.fabrikam.com/Extension1/</MoreInfo>
    <License>eula.rtf</License>
    <ReleaseNotes>notes.txt</ReleaseNotes>
    <Icon>Images\icon.png</Icon>
    <PreviewImage>Images\preview.png</PreviewImage>
  </Metadata>
  <Installation InstalledByMsi="false" AllUsers="false" SystemComponent="false" Scope="ProductExtension">
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="[11.0, 12.0]" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="[4.5,)" />
    <Dependency Id="Microsoft.VisualStudio.MPF.12.0" DisplayName="Visual Studio MPF 12.0" d:Source="Installed" Version="[12.0]" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.VsPackage" d:Source="Project" d:ProjectName="%CurrentProject%" Path="|%CurrentProject%;PkgdefProjectOutputGroup|" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>関連項目

- [出荷のビジュアル スタジオ拡張機能](../extensibility/shipping-visual-studio-extensions.md)
