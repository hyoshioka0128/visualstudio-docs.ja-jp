---
title: '方法: VSIX パッケージに依存関係を追加する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: b7ee7cbc4dee800351689386056389d274e07f4f
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012231"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>方法: VSIX パッケージに依存関係を追加する

ターゲットコンピューターにまだ存在しないすべての依存関係をインストールする VSIX パッケージの配置を設定できます。 これを実現するには、VSIX の依存関係を *source.extension.vsixmanifest* ファイルに追加します。

## <a name="to-add-a-dependency"></a>依存関係を追加するには

1. **デザイン**ビューで*source.extension.vsixmanifest*ファイルを開きます。 [ **依存関係** ] タブにアクセスし、[ **新規**] をクリックします。

2. インストールされている拡張機能を追加するには、[ **新しい依存関係の追加** ] ダイアログボックスで [ **インストールされている拡張機能** ] を選択し、[ **名前**] に一覧の拡張子を選択します。

3. インストールされていない別の VSIX を追加するには: [ **新しい依存関係の追加** ] ダイアログボックスで、[ **ファイルシステム上のファイル** ] を選択し、[ **参照** ] ボタンを使用して vsix を選択します。

## <a name="require-a-specific-visual-studio-release"></a>特定の Visual Studio リリースが必要

拡張機能に特定のバージョンの Visual Studio 2017 が必要な場合、たとえば、15.3 でリリースされた機能に依存している場合は、VSIX **インストールターゲット**でビルド番号を指定できます。 たとえば、リリース15.3 のビルド番号は ' 15.0.26730.3 ' です。 [ここで](../install/visual-studio-build-numbers-and-release-dates.md)は、リリースのマッピングを参照して番号を作成できます。 リリース番号 ' 15.3 ' を使用しても正常に機能しないことに注意してください。

拡張機能に15.3 以上が必要な場合は、 **Installationtarget バージョン** を [15.0.26730.3, 16.0) として宣言します。

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIXInstaller は、以前のバージョンの Visual Studio を検出し、後で更新する必要があることをユーザーに通知します。

## <a name="see-also"></a>関連項目

- [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [Windows インストーラー展開の拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)