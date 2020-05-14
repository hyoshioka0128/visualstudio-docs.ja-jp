---
title: '方法 : Visual Studio 拡張機能を更新する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 266c0a49db1bca03cec0eb68301445102173df3d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710664"
---
# <a name="how-to-update-a-visual-studio-extension"></a>方法 : 拡張機能を更新する
拡張機能**と更新**プログラムを使用して、更新されたバージョンをインストールすることで、システム上の Visual Studio 拡張機能を更新できます。 拡張機能の更新バージョンを作成する場合は、VSIX マニフェストのバージョン番号をインクリメントすることで、拡張機能を更新済みとして示すことができます。

 受信拡張機能の VSIX マニフェストがインストール済みと同じ`ID`で、より大きい`Version`番号が含まれている場合、更新プログラムがインストールされます。 番号が`Version`同じか、またはより低い場合、パッケージをインストールできません。 値が`ID`一致しない場合、まだインストールされていないパッケージは、別の拡張子として認識されます。

 開発中の競合を防ぐために、以前のバージョンの拡張機能をアンインストールし、競合する可能性のある拡張機能をアンインストールまたは無効化することをお勧めします。

## <a name="to-update-an-extension-on-your-system"></a>システムの拡張機能を更新するには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. 左側のウィンドウで、[**更新]** をクリックします。

3. 中央のウィンドウで、インストールする更新プログラムをクリックします。

     更新された拡張機能のバージョン番号が、右側のウィンドウに表示され、その他の情報も表示されます。

4. 右側のウィンドウの下部にある [**更新**] をクリックします。

## <a name="to-publish-an-update-of-an-extension"></a>拡張機能の更新を公開するには

1. Visual Studio で、更新する拡張機能のソリューションを開きます。 変更を行います。

    > [!IMPORTANT]
    > 署名なしすべてのユーザー拡張機能は自動的に更新されません。 拡張機能には常に署名する必要があります。

2. **ソリューション エクスプローラー**で、*ソース.extension.マニフェスト*を開きます。

3. マニフェスト デザイナーで、[**バージョン**] フィールドの数値を増やします。

4. ソリューションを保存してビルドします。

5. 新しい *.vsix*ファイル (プロジェクトの *\bin\Debug\*フォルダー内) を Visual Studio[マーケットプレース](https://marketplace.visualstudio.com/vs)Web サイトにアップロードします。

     拡張機能の以前のバージョンを持つユーザーが **[拡張機能と更新]** を開くと、ツールが自動的に更新プログラムを検索するように設定されている場合は、新しいバージョンが **[更新プログラム**] リストに表示されます。

     更新プログラムの自動チェックは**Tools** > **Options** > **Environment** > 、[**更新プログラム**] ウィンドウの下部 (**利用可能な更新プログラムの自動検出を有効または無効**にする)**Check for updates**で有効または無効に**できます。**

    > [!NOTE]
    > Visual Studio 2015 Update 2 以降では、ユーザーごとの拡張機能、すべてのユーザー拡張機能、またはその両方 (既定の設定) の自動更新を必要とするかどうかを **([ツール** > **オプション** > **のオプションの環境の** > **拡張機能と更新プログラム**] で) 指定できます。

## <a name="see-also"></a>関連項目
- [VSIX パッケージの解剖学](../extensibility/anatomy-of-a-vsix-package.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
