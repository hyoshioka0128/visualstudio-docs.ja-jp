---
title: VSIX パッケージのローカライズ |Microsoft Docs
description: 各ターゲット言語の vsixlangpack ファイルを作成し、適切なフォルダーに配置することによって、VSIX パッケージをローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d55acd30a0ea5381e9b14cf10c952c5626922c22
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893608"
---
# <a name="localizing-vsix-packages"></a>VSIX パッケージのローカライズ

各ターゲット言語の *vsixlangpack* ファイルを作成し、適切なフォルダーに配置することによって、VSIX パッケージをローカライズできます。 ローカライズされたパッケージをインストールすると、拡張機能のローカライズされた名前がローカライズされた説明と共に表示されます。 ローカライズされたライセンスファイル、またはローカライズされた情報を示す URL を指定すると、それらも表示されます。

VSIX パッケージの内容に、メニューコマンドやその他の UI を追加する VSPackage が含まれている場合は、新しい UI 要素のローカライズについて、「 [メニューコマンドのローカライズ](../extensibility/localizing-menu-commands.md) 」を参照してください。

## <a name="directory-structure"></a>ディレクトリの構造

 ユーザーが拡張機能をインストールすると、 **拡張機能と更新プログラム** によって、ターゲットコンピューターの Visual Studio ロケールに一致する名前を持つフォルダーの VSIX パッケージの最上位レベルがチェックされます。 **拡張機能と更新プログラム** によってフォルダー内の *vsixlangpack* ファイルが検出されると、そのファイル内のローカライズされた値が、 *source.extension.vsixmanifest* ファイル内の対応する値に置き換えられます。 これらの値は、拡張機能をインストールするときに表示されます。 次の例は、スペイン語 (es) とフランス語 (fr-fr) にローカライズされた VSIX パッケージのディレクトリ構造を示しています。

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
> Vsix でサポートされているプロジェクトテンプレートでは、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] vsix マニフェストを生成し、それに *source.extension.vsixmanifest* という名前を指定します。 Visual Studio によってプロジェクトがビルドされると、そのファイルの内容が VSIX パッケージの Source.extension.vsixmanifest にコピーされます。

## <a name="the-extensionvsixlangpack-file"></a>Vsixlangpack ファイル

*Vsixlangpack* ファイルは、 [VSIX 言語パックのスキーマ 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md)に従います。 このスキーマにはがあり `PackageLanguagePackManifest` 、その直後に `Metadata` 子要素が続きます。 メタデータ要素には、最大6つの子要素、、、、、、およびを含めることができ `DisplayName` `Description` `MoreInfo` `License` `ReleaseNotes` `Icon` ます。 これらの子要素は `DisplayName` 、 `Description` `MoreInfo` `License` `ReleaseNotes` `Icon` `Metadata` *source.extension.vsixmanifest* ファイルの要素の、、、、、およびの各子要素に対応します。

Vsixlangpack ファイルを作成する場合は、プロパティをに設定する必要があり `Include in Vsix` `true` ます。 それ以外の場合、ローカライズされたインストールテキストは無視されます。

### <a name="to-set-the-include-in-vsix-property"></a>[Vsix に含める (Vsix に含める) プロパティを設定するには

1. **ソリューションエクスプローラー** で、vsixlangpack ファイルを右クリックし、[**プロパティ**] をクリックします。

2. **プロパティグリッド** で、[ **Vsix に含める**] をクリックし、値をに設定し `true` ます。

## <a name="example"></a>例

### <a name="description"></a>説明

次の例は、 *source.extension.vsixmanifest* ファイルの関連部分を示しています。 このファイルには、スペイン語用の対応する *vsixlangpack* ファイルも含まれています。 ターゲットコンピューターの Visual Studio ロケールがスペイン語に設定されている場合は、言語パックの値によってマニフェストの値が置き換えられます。

### <a name="code"></a>コード

- [*Source.extension.vsixmanifest*]

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

- [*Vsixlangpack*]

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
|[VSIX 言語パックスキーマ2.0 リファレンス](vsix-language-pack-schema-2-0-reference.md)|VSIX 言語パックには、.vsix 展開ファイルのローカライズ情報が記述されています。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|Vsix パッケージの構造と内容について説明します。|
|[メニューコマンドのローカライズ](../extensibility/localizing-menu-commands.md)|拡張機能内の他のテキストリソースをローカライズする方法について説明します。|
