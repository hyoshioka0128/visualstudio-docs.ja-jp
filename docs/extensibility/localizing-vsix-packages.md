---
title: VSIX パッケージのローカライズ |マイクロソフトドキュメント
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d2d4222e45d56447951e86d558af9983a0d1cc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702899"
---
# <a name="localizing-vsix-packages"></a>VSIX パッケージのローカライズ

VSIX パッケージをローカライズするには、各ターゲット言語の*Extension.vsixlangpack*ファイルを作成し、正しいフォルダーに配置します。 ローカライズされたパッケージがインストールされると、ローカライズされた拡張機能の名前がローカライズされた説明と共に表示されます。 ローカライズされたライセンス ファイル、またはローカライズされた情報を指す URL を指定すると、そのファイルも表示されます。

VSIX パッケージにメニュー コマンドまたはその他の UI を追加する VSPackage が含まれているコンテンツの場合は、新しい UI 要素のローカライズ方法については、「[メニュー コマンド](../extensibility/localizing-menu-commands.md)のローカライズ」を参照してください。

## <a name="directory-structure"></a>ディレクトリの構造

 ユーザーが拡張機能をインストールすると、**拡張機能と更新プログラム**は、VSIX パッケージの最上位レベルで、ターゲット コンピューターの Visual Studio ロケールと名前が一致するフォルダーを確認します。 **拡張機能と更新プログラム**がフォルダー内の *.vsixlangpack*ファイルを見つける場合は、そのファイル内のローカライズされた値を *.vsixmanifest*ファイル内の対応する値に置き換えます。 これらの値は、拡張機能のインストール時に表示されます。 次の例は、スペイン語 (es-ES) およびフランス語 (fr-FR) にローカライズされた VSIX パッケージのディレクトリ構造を示しています。

```text
.
├── MyExtension.dll
├── Extension.vsixmanifest
├── [Content_Types].xml
├── es-ES
│   └── Extension.vsixlangpack
└── fr-FR
    └── Extension.vsixlangpack
```

> [!NOTE]
> VSIX でサポートされているプロジェクト テンプレート[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]は、VSIX マニフェストを生成し、その名前を*source.extension.vsixmanifest と指定します*。 Visual Studio は、プロジェクトをビルドするときに、そのファイルの内容を VSIX パッケージ内の Extension.VsixManifest にコピーします。

## <a name="the-extensionvsixlangpack-file"></a>ファイルの拡張子.vsixlangpack

*拡張.vsixlangpack*ファイルは[、VSIX 言語パックスキーマ 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md)に従います。 このスキーマには、`PackageLanguagePackManifest`の直後に子要素が`Metadata`続きます。 メタデータ要素には、最大 6 つの`DisplayName`子要素、、、、、、、、、、`Description``MoreInfo``License`および`ReleaseNotes`を含めることができます。 `Icon` これらの子要素`DisplayName`は、`Description`*拡張.vsixmanifest*ファイル`Icon`の`Metadata`要素の 、 、 `MoreInfo` `License`、、`ReleaseNotes`および子要素に対応します。

vsixlangpack ファイルを作成する場合は、プロパティを`Include in Vsix`に`true`設定する必要があります。 それ以外の場合、ローカライズされたインストール テキストは無視されます。

### <a name="to-set-the-include-in-vsix-property"></a>プロパティに含めるプロパティを設定するには

1. **ソリューション エクスプローラー**で、Extension.vsixlangpack ファイルを右クリックし、[**プロパティ**] をクリックします。

2. [**プロパティ グリッド**] で **、[Vsix に含める**]`true`をクリックし、値を に設定します。

## <a name="example"></a>例

### <a name="description"></a>説明

次の例は *、Extension.vsixmanifest*ファイルの関連部分を示しています。 ファイルには、対応するスペイン語用*の拡張子.vsixlangpack*ファイルも含まれています。 ターゲット コンピューターの Visual Studio ロケールがスペイン語に設定されている場合、言語パックの値は、マニフェストの値を置き換えます。

### <a name="code"></a>コード

- [*拡張機能.vsixmanifest*]

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest ...>
  <Metadata ...>
    <DisplayName>Family Tree</DisplayName>
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>
    <MoreInfo>http://www.contoso.com/products/FamilyTree.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
  <Installation .../>
  <Dependencies .../>
  <Prerequisites .../>
  <Assets .../>
</PackageManifest>
```

- [*エクステンション.vsixlangpack*]

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</DisplayName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>関連項目

|Title|説明|
|-----------|-----------------|
|[VSIX 言語パック スキーマ 2.0 リファレンス](vsix-language-pack-schema-2-0-reference.md)|VSIX 言語パックは、.vsix デプロイメント ファイルのローカライズ情報を記述します。|
|[VSIX パッケージの解剖学](../extensibility/anatomy-of-a-vsix-package.md)|vsix パッケージの構造と内容について説明します。|
|[ローカライズ メニュー コマンド](../extensibility/localizing-menu-commands.md)|拡張機能内の他のテキスト リソースをローカライズする方法を示します。|
