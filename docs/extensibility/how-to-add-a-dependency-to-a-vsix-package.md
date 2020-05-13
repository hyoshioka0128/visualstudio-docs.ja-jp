---
title: '方法 : VSIX パッケージに依存関係を追加する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f8b350f063c28762edf90edfe71330534451c75d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711078"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>方法: VSIX パッケージに依存関係を追加する

ターゲット コンピューターに存在しない依存関係をインストールする VSIX パッケージの配置を設定できます。 これを実現するには、*ソース.extension.vsixmanifestファイルへのVSIX依存関係を含めます*。

## <a name="to-add-a-dependency"></a>依存関係を追加するには

1. **デザイン**ビューで *、ソース.extension.vsixmanifest*ファイルを開きます。 [**依存関係**] タブに移動し、[**新規**] をクリックします。

2. インストール済みの拡張機能を追加するには、次に[**新しい依存関係の追加**] ダイアログ ボックスで [**インストールされた拡張機能**] を選択し、[**名前**] ボックスの一覧で拡張機能を選択します。

3. インストールされていない別の VSIX を追加するには、[**新しい依存関係の追加**] ダイアログ ボックスで [**ファイル オン ファイル**] を選択し、[**参照**] ボタンを使用して VSIX を選択します。

## <a name="require-a-specific-visual-studio-release"></a>特定の Visual Studio リリースを必要とする

たとえば、拡張機能で Visual Studio 2017 の特定のバージョンが必要な場合は、15.3 でリリースされた機能に依存し、VSIX**インストール ターゲット**でビルド番号を指定できます。 たとえば、リリース 15.3 のビルド番号は '15.0.26730.3' です。 番号を構築するためのリリースのマッピングは、[ここ を参照してください](../install/visual-studio-build-numbers-and-release-dates.md)。 リリース番号 '15.3' を使用すると、正しく動作しないことに注意してください。

拡張に 15.3 以上が必要な場合は **、InstallationTarget バージョン**を [15.0.26730.3, 16.0:

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIX インストーラーは、以前のバージョンの Visual Studio を検出し、後の更新プログラムが必要であることをユーザーに通知します。

## <a name="see-also"></a>関連項目

- [VSIX 拡張スキーマ 1.0 リファレンス](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
- [VSIX パッケージの解剖学](../extensibility/anatomy-of-a-vsix-package.md)
- [Windows インストーラの展開用の拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
