---
title: VSIX 言語パックスキーマ2.0 リファレンス |Microsoft Docs
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
author: acangialosi
ms.author: anthc
manager: jillfra
ms.openlocfilehash: f0eee51c0654c6e517209e23baf43c6b262d8f73
ms.sourcegitcommit: c31815e140f2ec79e00a9a9a19900778ec11e860
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91830705"
---
# <a name="vsix-language-pack-schema-20-reference"></a>VSIX 言語パックスキーマ2.0 リファレンス

VSIX 言語パックのスキーマには、VSIX パッケージのローカライズされたインストール情報が含まれています。 このスキーマのバージョン2.0 では、追加のローカライズ要素がサポートされています。

## <a name="language-pack-schema"></a>言語パックスキーマ

言語パックファイルのルート要素はであり、 `<PackageLanguagePackManifest>` の属性は `Version` 言語パック形式のバージョンです。 この記事では、言語パック形式のバージョン2.0 について説明します。これは、属性を値に設定することによってマニフェストで指定し `Version` `Version="2.0.0"` ます。 ルート要素には、1つの子要素のみが含まれ `<Metadata>` ます。

### <a name="packagelanguagepackmanifest-element"></a>PackageLanguagePackManifest 要素

要素内に `<PackageLanguagePackManifest>` は、次の要素が存在している必要があります。

|タイトル|説明|
|-----------|-----------------|
|`<Metadata>`| ローカライズされたすべてのパッケージメタデータのコンテナー要素

### <a name="metadata-element"></a>Metadata 要素

要素内には `<Metadata>` 、次の要素を含めることができます。

|タイトル|説明|
|-----------|-----------------|
|`<DisplayName>`|インストールする拡張機能のローカライズされた名前|
|`<Description>`|インストールする拡張機能のローカライズされた説明|
|`<License>`| 拡張機能のライセンスのローカライズ版へのパス|
|`<MoreInfo>`| 拡張機能に関するローカライズされた情報へのリンク|
|`<ReleaseNotes>`| リリースノートのパスまたはローカライズされたバージョンへのリンク|
|`<Icon>`| 拡張機能アイコンのローカライズ版へのパス|

### <a name="sample-manifest"></a>サンプル マニフェスト

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
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|VSIX パッケージのローカライズされたインストールをサポートする方法を示します。|
|[VSIX 拡張機能スキーマ2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)|VSIX マニフェストは、 *.vsix* 配置ファイルの内容を記述します。 配置ファイルを使用すると、[ **拡張機能と更新プログラム** ] ダイアログボックスを使用して、Visual Studio 拡張機能をインストールできます。|
|[Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)|[ **拡張機能と更新プログラム** ] ダイアログボックスを使用して、拡張機能のインストール、削除、アクティブ化、および非アクティブ化を行う方法について説明します。|
