---
title: Windows インストーラーパッケージを作成する |Microsoft Docs
description: ファイルとレジストリデータを含むデータベーステーブルで構成される Visual Studio の Windows インストーラーパッケージを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 445b302c66739c8a35f180686011f3b498f87ada
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906131"
---
# <a name="author-a-windows-installer-package"></a>Windows インストーラーパッケージを作成する
データは Windows インストーラーモデルを駆動します。 たとえば、ファイルをコピーしてレジストリエントリを書き込むための手続き型スクリプトを記述するのではなく、ファイルとレジストリデータを格納するデータベーステーブルの行と列を作成します。

## <a name="database-entries"></a>データベースエントリ
VSPackage をインストールするには、Windows インストーラーパッケージに次のタスクを実行するためのデータベースエントリが含まれている必要があります。

- システムを検索して、サポートされている VSPackage のバージョンを探し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます (AppSearch、CompLocator、RegLocator、DrLocator、署名を含む Windows インストーラーテーブルを使用します)。

- サポートされているのバージョンがインストールされていない場合、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] または VSPackage の別のシステム要件が満たされていない場合 (LaunchCondition テーブルを使用)、インストールをキャンセルします。

- ディレクトリ、コンポーネント、およびファイルテーブルを使用して、VSPackage ファイルと依存ファイルをインストールします。

- VSPackage の適切な情報をレジストリに追加します (レジストリテーブルを使用します)。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)](CustomAction テーブルを使用して) **devenv.exe のセットアップ** を呼び出して、の VSPackage を統合します。

詳細については、「 [Windows インストーラー](/windows/desktop/Msi/windows-installer-portal)」を参照してください。

## <a name="setup-tools"></a>セットアップツール
さまざまなサードパーティ製セットアップツールは、Windows インストーラーパッケージの開発環境を提供します。 次の無料ツールを利用できます。

- InstallShield 制限付きエディション

   Visual Studio の [ **新しいプロジェクト** ] ダイアログボックスでは、InstallShield の限定バージョンを取得できます。 [ **その他のプロジェクトの種類** ] を展開し、[ **セットアップと配置**] を選択します。 InstallShield テンプレートを選択します。

- Windows インストーラー XML ツールセット

   Windows インストーラー XML (WiX) ツールセットは、XML ソースファイルからパッケージを Windows インストーラービルドします。 WiX ツールセットは、Microsoft オープンソースプロジェクトです。 [Wix ツールセット](https://sourceforge.net/projects/wix/)からソースコードと実行可能ファイルをダウンロードできます。

   を使用してに統合する商用製品の場合は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 、「 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)」を参照してください。

## <a name="see-also"></a>関連項目
- [Windows インストーラーと共に Vspackage をインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
