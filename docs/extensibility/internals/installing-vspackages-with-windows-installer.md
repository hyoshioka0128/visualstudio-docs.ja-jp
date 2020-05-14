---
title: Windows インストーラを使用した VS パッケージのインストール |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2eb90dbffa9f04cd17afa70d2bdfc59205bc99cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707462"
---
# <a name="installing-vspackages-with-windows-installer"></a>Windows インストーラーによる VSPackage のインストール
VSPackage をに[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合するには、ユーザーのコンピューターにファイルをコピーするだけではありません。 VSPackage のインストーラーは、VSPackage とその依存ファイルをインストールし、登録し、に統合[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]する必要があります。 VSPackage は、スプラッシュ スクリーンや [情報] ダイアログ ボックス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]にアイコンを表示するなどの統合機能を利用できます。

 マイクロソフトの Windows インストーラー ファイルは、VS パッケージを配布する推奨される方法です。 使いやすい Windows インストーラ パッケージは、 で[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]サポートされている任意の Windows オペレーティング システムで実行できます。 詳細については、「 [Windows インストーラ](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [Windows インストーラーの基本事項](../../extensibility/internals/windows-installer-basics.md)

 Windows インストーラの概要を説明します。

- [VSPackage のセットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)

 VSPackages と[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の両方のサイド バイ サイド インストールをサポートするさまざまな方法について説明します。

- [Windows インストーラー パッケージの編集](../../extensibility/internals/authoring-a-windows-installer-package.md)

 VSPackages を正しくインストールして に統合するために、インストーラーが従う一[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]般的な手順の概要を示します。

- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)

 VSPackage の要件が満[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]たされていない場合にインストーラーが検出し、そのコンポーネントを検出し、セットアップをキャンセルする方法について説明します。

- [コンポーネント管理](../../extensibility/internals/component-management.md)

 以前の製品バージョンの整合性を維持するインストーラの開発方法について説明します。

- [VSPackage のインストール ディレクトリの選択](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 VSPackages を検索するためのオプションを要約します。

- [VSPackage の登録](../../extensibility/internals/vspackage-registration.md)

 インストール時に VSPackage を登録する方法と、自己登録が不適切な理由について説明します。

- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)

 マネージ コード プロジェクトの種類に対して新しいプロジェクト型のアグリゲーターを使用する方法について説明します。

- [方法: インストーラー向けの登録情報の生成](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 RegPkg.exe を使用して、マネージ VSPackage の登録マニフェストを生成する方法について説明します。

- [インストール後に実行する必要があるコマンド](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 インストール後のコマンドを実行して VSPackages を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に統合する方法について説明します。

- [Windows インストーラーによる VSPackage のアンインストール](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 ユーザーが VSPackage をアンインストールするときにインストーラーで実行する必要がある手順について説明します。
