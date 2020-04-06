---
title: VSIX プロジェクト テンプレート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74791a77ee1c720fb60876a1efa6bd58fa94f68b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697935"
---
# <a name="vsix-project-template"></a>VSIX プロジェクト テンプレート

VSIX プロジェクト テンプレートを使用して、1 つ以上の Visual Studio 拡張機能を VSIX プロジェクトにラップし、パッケージを[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)Web サイトに発行できます。

 VSIX 配置では、VSPackage、アセンブリ、MEF コンポーネント、プロジェクト テンプレート、項目テンプレート、ツールボックス コントロール、およびカスタム拡張機能の種類がサポートされています。

> [!NOTE]
> VSIX プロジェクトを使用するには、Visual Studio SDK をインストールする必要があります。 Visual Studio SDK の詳細については[、「Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="where-to-find-the-vsix-project-template"></a>VSIX プロジェクト テンプレートの場所

VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログ ボックスで使用できます。  C# と Visual Basic の両方のバージョンがあります。

> [!TIP]
> [**新しいプロジェクト**] ダイアログの上部にあるドロップダウン リスト ボックスで 、.NET Framework 4.5 以降が指定されていることを確認してください。

## <a name="uses-of-the-vsix-project-template"></a>VSIX プロジェクト テンプレートの使用

VSIX プロジェクト テンプレートには、主に次の 2 つの用途があります。

- プロジェクト テンプレート、項目テンプレート、および拡張機能を配置します。

- 複数の拡張機能の出力を 1 つの展開パッケージにラップする。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>空の VSIX プロジェクトに拡張機能をパッケージ化する

空の VSIX プロジェクトにラップすることで、既存の拡張機能、または VSIX サポートがまだない拡張機能をパッケージ化できます。 ラップする拡張機能は[、VSIX スキーマ](../extensibility/vsix-extension-schema-2-0-reference.md)でサポートされている型である必要があります。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>VSIX プロジェクトを使用して拡張機能をパッケージ化するには

1. 拡張機能を構成するプロジェクトをビルドします。

2. VSIX プロジェクト テンプレートを使用して**VSIX プロジェクト**を作成します。

    *マニフェスト***デザイナー**で開きます。

3. [**アセット**] タブで、[**新規**] ボタンを選択します。

    [**新しいアセットの追加**] ダイアログ ボックスが表示されます。

4. [**種類]** ボックスの一覧で、追加する拡張機能の種類を選択します。

5. 現在のソリューションに含まれる拡張機能またはコンテンツ要素 (項目テンプレートやコンパイル済みアセンブリなど) を追加するには、次の手順に従います。

   1. [**ソース**] ボックスの一覧**で、[現在のソリューションのプロジェクト**] を選択します。

   2. [**プロジェクト**] ボックスの一覧で、拡張機能の名前を選択します。

   3. [**このフォルダに埋め込む**] ボックスに、アセットを埋め込むフォルダの名前を入力し **、[OK] を**クリックします。

6. 現在のソリューションに含まれていない拡張機能またはコンテンツ要素を追加するには、次の手順を実行します。

   1. [**ソース**] リスト ボックス**で、[ファイル システム上のファイル**] を選択します。

   2. [**パス**] フィールドに、コンパイルまたは圧縮された拡張ファイルへの完全パスを入力するか、[**参照]** ボタンを使用してファイルを参照します。

   3. [**このフォルダに埋め込む**] ボックスに、アセットを埋め込むフォルダの名前を入力し **、[OK] を**クリックします。

7. パッケージに追加の拡張機能を含める場合は、同じ方法で追加します。

8. ソリューションをビルドします。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSIX マニフェスト ファイル 、[Content_Types]*.xml*ファイル、およびプロジェクトに追加したすべての拡張資産を含む *.vsix*ファイルをビルドします。

## <a name="see-also"></a>関連項目

- [VSIX 拡張スキーマ 2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
