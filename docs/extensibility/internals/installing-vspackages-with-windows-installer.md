---
title: Windows インストーラーを使用した Vspackage のインストール |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707462"
---
# <a name="installing-vspackages-with-windows-installer"></a>Windows インストーラーによる VSPackage のインストール
VSPackage をに統合するに [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、ユーザーのコンピューターにファイルをコピーするだけではありません。 VSPackage のインストーラーは、VSPackage とその依存ファイルをインストールし、それらをに登録して統合する必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 VSPackage は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] スプラッシュスクリーンと [バージョン情報] ダイアログボックスにアイコンを表示するなどの統合機能を利用できます。

 Vspackage を配布するには、Microsoft Windows インストーラーファイルを使用することをお勧めします。 使いやすい Windows インストーラーパッケージは、でサポートされている任意の Windows オペレーティングシステムで実行でき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 詳細については、「 [Windows インストーラー](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [Windows インストーラーの基本事項](../../extensibility/internals/windows-installer-basics.md)

 Windows インストーラーの概要について説明します。

- [VSPackage のセットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)

 Vspackage との両方のサイドバイサイドインストールをサポートするさまざまな方法について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [Windows インストーラー パッケージの編集](../../extensibility/internals/authoring-a-windows-installer-package.md)

 Vspackage を正しくインストールして統合するための一般的な手順インストーラーの概要について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage の要件が満たされていない場合に、インストーラーがコンポーネントとそのコンポーネントを検出し、セットアップをキャンセルする方法について説明します。

- [コンポーネント管理](../../extensibility/internals/component-management.md)

 以前の製品バージョンの整合性を維持するインストーラーを開発する方法について説明します。

- [VSPackage のインストール ディレクトリの選択](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 Vspackage を検索するためのオプションの概要を示します。

- [VSPackage の登録](../../extensibility/internals/vspackage-registration.md)

 インストール時に Vspackage を登録する方法と、自己登録が正しくない理由について説明します。

- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)

 マネージコードプロジェクトの種類に新しいプロジェクトタイプアグリゲーターを使用する方法について説明します。

- [方法: インストーラー向けの登録情報の生成](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 RegPkg.exe を使用して、マネージ VSPackage の登録マニフェストを生成する方法について説明します。

- [インストール後に実行する必要があるコマンド](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 インストール後のコマンドを実行して Vspackage をに統合する方法について説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

- [Windows インストーラーによる VSPackage のアンインストール](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 ユーザーが VSPackage をアンインストールするときにインストーラーで実行する必要がある手順について説明します。
