---
title: '方法: Visual Studio 拡張機能を更新する |Microsoft Docs'
description: 拡張機能と更新プログラムを使用して、更新されたバージョンをインストールすることによって、システムの Visual Studio 拡張機能を更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: be22ca13fd5af8df88501835c8a030cc6469e179
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995605"
---
# <a name="how-to-update-a-visual-studio-extension"></a>方法: Visual Studio 拡張機能を更新する
**拡張機能と更新プログラム** を使用して、更新されたバージョンをインストールすることにより、システムの Visual Studio 拡張機能を更新できます。 更新されたバージョンの拡張機能を作成した場合は、VSIX マニフェストのバージョン番号をインクリメントして、更新されたバージョンを示すことができます。

 更新プログラムがインストールされるのは、受信拡張機能の VSIX マニフェストが、 `ID` インストールされている1つ以上の数値と同じ場合 `Version` です。 `Version`数値が同じかそれより小さい場合は、パッケージをインストールできません。 値が一致しない場合 `ID` 、まだインストールされていないパッケージは個別の拡張機能として認識されます。

 開発中の競合を防ぐために、実行中の拡張機能の以前のバージョンをアンインストールすることをお勧めします。また、競合している可能性のある拡張機能をアンインストールまたは無効にすることをお勧めします。

## <a name="to-update-an-extension-on-your-system"></a>システムの拡張機能を更新するには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. 左側のウィンドウで、[ **更新**] をクリックします。

3. 中央のウィンドウで、インストールする更新プログラムをクリックします。

     更新された拡張機能のバージョン番号が、その他の情報と共に右側のウィンドウに表示されます。

4. 右側のウィンドウの下部にある [ **更新**] をクリックします。

## <a name="to-publish-an-update-of-an-extension"></a>拡張機能の更新プログラムを公開するには

1. Visual Studio で、更新する拡張機能のソリューションを開きます。 変更を行います。

    > [!IMPORTANT]
    > 署名されていないすべてのユーザー拡張機能は自動的に更新されません。 常に拡張機能に署名する必要があります。

2. **ソリューションエクスプローラー** で、[*ソース] 拡張子 .manifest* を開きます。

3. マニフェストデザイナーで、[ **バージョン** ] フィールドの値を大きくします。

4. ソリューションを保存してビルドします。

5. 新しい *.vsix* ファイル ( \* プロジェクトの * \bin\debug フォルダー内) を [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) Web サイトにアップロードします。

     以前のバージョンの拡張機能を使用しているユーザーが **拡張機能と更新プログラム** を開くと、ツールが自動的に更新プログラムを検索するように設定されている場合、新しいバージョンが **更新プログラム** の一覧に表示されます。

     更新プログラムの自動確認を有効または無効にすることができます (**利用可能な更新プログラムの自動検出を有効** または無効にします)。これにより、[**ツール** オプション] の [   >    >  **環境**  >  **拡張機能と更新プログラム**] で [更新プログラムのチェック] 設定が変更されます。

    > [!NOTE]
    > Visual Studio 2015 Update 2 以降では、   >    >    >  ユーザー単位の拡張機能、すべてのユーザー拡張機能、またはその両方 (既定の設定) に対して自動更新を実行するかどうかを指定できます ([ツールオプション] [環境 **拡張機能と更新プログラム**])。

## <a name="see-also"></a>こちらもご覧ください
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
