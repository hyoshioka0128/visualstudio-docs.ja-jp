---
title: Visual Studio 2017 SDK の新機能&#39;|マイクロソフトドキュメント
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 88330aa68f2a3752431fd2fbe6c5c1c649acbb8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697206"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK の新機能&#39;

Visual Studio SDK には、Visual Studio 2017 の次の新機能と更新された機能があります。

## <a name="vsix-v3-format"></a>VSIX v3 形式

Visual Studio 2017 の新しい軽量インストールをサポートするために、VSIX 拡張機能マニフェストの形式がバージョン 3 (VSIX v3) に更新されました。

新しい形式では、次の機能がサポートされています。

* VSIX インストーラによって検出およびインストールされる必須コンポーネントを明示的に宣言します。
* 拡張インストール時の Ngen アセンブリ。
* 通常の拡張ルートの外部にアセットをインストールする。

これらの変更の詳細については、次のトピックを参照してください。

* [Visual Studio 2017 の機能拡張の変更点](breaking-changes-2017.md)
* [VSIX v3 での Ngen のサポート](ngen-support.md)
* [拡張機能フォルダー外でのインストール](set-install-root.md)
* [Visual Studio 2017 の拡張機能に関するよく寄せられる質問](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>拡張機能プロジェクトを Visual Studio 2017 に移行する

拡張機能プロジェクトとその VSIX マニフェストを Visual Studio 2017 に更新する方法については、「[方法: 拡張機能プロジェクトを Visual Studio 2017 に移行する](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)」を参照してください。

## <a name="custom-project-and-item-templates"></a>カスタム プロジェクトテンプレートと項目テンプレート

Visual Studio 2017 以降、カスタム プロジェクトと項目テンプレートのスキャンは実行されなくなります。 代わりに、拡張機能は、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Visual Studio 2017 を使用して、VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手入力で生成する必要があります。 詳細については、「 [Visual Studio 2017 のカスタム プロジェクトテンプレートと項目テンプレートをアップグレードする](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)」を参照してください。 テンプレート マニフェスト スキーマについては、「 [Visual Studio テンプレート マニフェスト スキーマ リファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」に記載されています。

## <a name="updated-extension-performance-guidelines"></a>拡張機能のパフォーマンス ガイドラインを更新しました

Visual Studio の起動時間とソリューションの読み込み時間に対する拡張機能の影響を検出して分析する方法を示す方法を示す[VSPackage](managing-vspackages.md)の管理の下に新しい[方法: 拡張機能のパフォーマンス](how-to-diagnose-extension-performance.md)の記事があります。
