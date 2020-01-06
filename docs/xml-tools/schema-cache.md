---
title: XML エディタースキーマキャッシュ
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 35a7fcad-f3bf-4a96-9008-4306e7276223
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40781a5249d9b69df5f41f863f3d36ac6a119645
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592491"
---
# <a name="schema-cache"></a>スキーマ キャッシュ

XML エディターは、 *%VSInstallDir%\xml\Schemas*ディレクトリにあるスキーマキャッシュを提供します。 スキーマキャッシュは、コンピューター上のすべてのユーザーに対してグローバルであり、IntelliSense および XML ドキュメントの検証に使用される標準の XML スキーマが含まれています。

XML エディターでは、ソリューションに配置されているスキーマ、ドキュメントの **[プロパティ]** ウィンドウの **[スキーマ]** フィールドで指定したスキーマ、および `xsi:schemaLocation` 属性と `xsi:noNamespaceSchemaLocation` 属性で識別されるスキーマも検索できます。

次の表では、XML エディターと共にインストールされるスキーマについて説明します。

| Filename | 説明 |
|-| - |
| *catalog.xsd* | XML エディターのスキーマ カタログ ファイル用のスキーマです。 スキーマ カタログの詳細については、下記を参照してください。 |
| *DotNetConfig .xsd* | Web.config ファイルのスキーマ、`http://schemas.microsoft.com/.NETConfiguration/v2.0`。 |
| *msbuild.exe* | MSBuild の make ファイルのスキーマ、`http://schemas.microsoft.com/developer/msbuild/2003`。 |
| *msdata.xsd* | <xref:System.Data.DataSet> クラスによって追加される XSD 注釈用のスキーマ (urn:schemas-microsoft-com:xml-msdata) です。 |
| *msxsl.xsd* | Microsoft XSLT スクリプト ブロック拡張用のスキーマ (urn:schemas-microsoft-com:xslt) です。 |
| *SnippetFormat* | コード スニペットの XML ファイルのスキーマです。 例については、「 *%VC#VSInstallDir% \ 展開*」を参照してください。 |
| *Soap 1.1. xsd* | Simple Object Access Protocol (SOAP) 1.1 のスキーマ、`http://schemas.xmlsoap.org/soap/envelope/`。 |
| *Soap 1.2. xsd* | 簡易オブジェクト アクセス プロトコル 1.2 のスキーマです。 |
| *SiteMapSchema* | ASP.NET sitemap XML ファイルのスキーマ、`http://schemas.microsoft.com/AspNet/SiteMap-File-1.0`。 |
| *wsdl.xsd* | Web サービス記述言語のスキーマ、`http://schemas.xmlsoap.org/wsdl/`。 |
| *xenc .xsd* | XML 暗号化のスキーマ、`http://www.w3.org/2000/09/xmldsig#`。 |
| *xhtml. xsd* | XHTML `http://www.w3.org/1999/xhtml`のスキーマ。 |
| *xlink* | XLink 1.0 のスキーマ、`http://www.w3.org/1999/xlink`。 |
| *xml .xsd* | Xml: space および xml: lang 属性、`http://www.w3.org/XML/1998/namespace`を記述するスキーマ。 |
| *xmlsig.xsd* | XML デジタル署名のスキーマ、`http://www.w3.org/2000/09/xmldsig#`。 |
| *xsdschema .xsd* | XSD 自体、`http://www.w3.org/2001/XMLSchema`を記述するスキーマ。 |
| *xslt.xsd* | XML 変換のスキーマ、`http://www.w3.org/1999/XSL/Transform`。 |

## <a name="update-schemas-in-the-cache"></a>キャッシュ内のスキーマを更新する

エディターは、XML エディター パッケージが読み込まれるときにスキーマ キャッシュのディレクトリを読み込み、実行中にはすべての変更点を監視します。 スキーマが追加された場合は、そのスキーマがメモリ内にある既知のスキーマのインデックス内に自働的に読み込まれます。 スキーマが削除された場合は、そのスキーマがメモリ内のインデックスから自働的に削除されます。 スキーマが更新された場合は、メモリ内にあるそのスキーマのキャッシュが自動的に無効化されます。

> [!NOTE]
> スキーマ キャッシュのディレクトリはコンピューター上でグローバルなので、このキャッシュには、コンピューター上で作成されるすべての Visual Studio プロジェクトに対して標準的かつ有用なスキーマのみを追加する必要があります。

XML エディターはまた、スキーマ キャッシュ ディレクトリ内で任意の数のスキーマ カタログ ファイルをサポートします。 スキーマ カタログでは、エディターで常に認識しておきたいスキーマが存在する他の場所を指し示すことができます。 *カタログの .xsd*ファイルは、カタログファイルの形式を定義し、スキーマキャッシュのディレクトリに含まれます。 *カタログ .xml*ファイルは既定のカタログであり、 *% VSInstallDir%* 内の他のスキーマへのリンクが含まれています。 次に、*カタログ .xml*ファイルのサンプルを示します。

```xml
<SchemaCatalog xmlns="http://schemas.microsoft.com/xsd/catalog">
  <Schema href="%VSInstallDir%/help/schemas/Favorites.xsd" targetNamespace="urn:Favorites-Schema"/>
  <Schema href="%VSInstallDir%/help/schemas/Links.xsd" targetNamespace="urn:Links-Schema"/>
  <Schema href="%VSInstallDir%/help/schemas/MyHelp.xsd" targetNamespace="urn:VSHelp-Schema"/>
</SchemaCatalog>
```

`href` 属性は、任意のファイル パスか、またはスキーマを指す http URL のいずれかになります。 ファイル パスとして、カタログ ドキュメントを基準にした相対パスを使用できます。 %% で区切られた次の変数は、エディターによって認識され、パスに展開されます。

- VSInstallDir

- System

- ProgramFiles

- ［プログラム］

- CommonProgramFiles

- ApplicationData

- CommonApplicationData

- LCID

カタログ ドキュメントには、他のカタログを指す `Catalog` 要素を含めることができます。 `Catalog` 要素を使用して、チームや会社で共有する集中管理カタログや、ビジネス パートナーと共有するオンライン カタログを指し示すことができます。 `href` 属性は、ファイル パスか、他のカタログの http URL です。 `Catalog` 要素の例を次に示します。

```xml
<Catalog href="file://c:/xcbl/xcblCatalog.xml"/>
```

カタログでは、特別な `Association` 要素を使用して、スキーマを XML ドキュメントと関連付ける方法を制御することもできます。 この要素は、ターゲットの名前空間を持たないスキーマを特定のファイル拡張子に関連付けます。これは、XML エディターが、`targetNamespace` 属性を持たないスキーマの自動関連付けを実行しないため便利です。 `Association` 要素によって、dotNetConfig スキーマを "config" というファイル拡張子を持つすべてのファイルと関連付ける例を次に示します。

```xml
<Association extension="config" schema="%VSInstallDir%/xml/schemas/dotNetConfig.xsd"/>
```

## <a name="localized-schemas"></a>ローカライズされたスキーマ

多くの場合、*カタログ .xml*ファイルにはローカライズされたスキーマのエントリが含まれていません。 ローカライズされたスキーマディレクトリを指す別のエントリを、 *catalog .xml*ファイルに追加できます。

次の例では、%LCID% 変数を使用してローカライズされたスキーマを指し示す新しい `Schema` 要素を作成します。

```xml
<Schema href="%InstallRoot%/Common7/IDE/Policy/Schemas/%LCID%/TDLSchema.xsd"
  targetNamespace="http://www.microsoft.com/schema/EnterpriseTemplates/TDLSchema"/>
```

## <a name="change-the-location-of-the-schema-cache"></a>スキーマキャッシュの場所の変更

[**その他**のオプション] ページを使用して、スキーマキャッシュの場所をカスタマイズできます。 よく使用するスキーマのディレクトリがある場合は、それらのスキーマを代わりに使用するようにエディターを構成できます。

> [!NOTE]
> この変更によって影響を受けるのは、現在の Visual Studio ユーザーのみです。

### <a name="to-change-the-schema-cache-location"></a>スキーマ キャッシュの場所を変更するには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[テキストエディター]** 、 **[XML]** の順に展開し、 **[その他]** をクリックします。

3. **[スキーマ]** フィールドの **[参照]** ボタンをクリックします。

4. スキーマキャッシュのフォルダーを選択し、[ **OK]** をクリックします。

### <a name="to-add-another-directory-of-common-schemas"></a>よく使用するスキーマが存在するディレクトリを追加するには

1. XML エディターのスキーマキャッシュディレクトリで、 *catalog .xml*ファイルを編集します。

2. 追加するスキーマのディレクトリを指し示す新しい `<Catalog href="..."/>` 要素を追加します。

3. 変更を [保存] します。

   カタログは自動的に再度読み込まれます。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
