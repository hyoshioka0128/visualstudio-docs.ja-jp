---
title: Windows インストーラ パッケージを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d30c0e2b3b375e6e0efedddd3a017fbfb8646a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710039"
---
# <a name="author-a-windows-installer-package"></a>Windows インストーラ パッケージを作成する
データは Windows インストーラ モデルを駆動します。 たとえば、ファイルをコピーしてレジストリ エントリを書き込むプロシージャ スクリプトを記述するのではなく、ファイルとレジストリ データを含むデータベース テーブルで行と列を作成します。

## <a name="database-entries"></a>データベースエントリ
VSPackage をインストールするには、Windows インストーラー パッケージには、次のタスクを実行するデータベース エントリが含まれている必要があります。

- システムを検索して VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]サポートされているバージョンを見つけます (アプリサーチ、コンパケータ、RegLocator、DrLocator、およびシグネチャを含む Windows インストーラー テーブルを使用)。

- サポートされているバージョンがインストールされていない場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]または VSPackage の別のシステム要件が満たされていない場合は、インストールをキャンセルします (LaunchCondition テーブルを使用)。

- VSPackage と依存ファイルをインストールします (ディレクトリ、コンポーネント、およびファイル テーブルを使用)。

- VSPackage の適切な情報をレジストリに追加します (レジストリ テーブルを使用)。

- (カスタムアクション テーブル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用して) **devenv.exe /setup**を呼び出すことによって、VSPackage を統合します。

詳細については、「 [Windows インストーラ](/windows/desktop/Msi/windows-installer-portal)」を参照してください。

## <a name="setup-tools"></a>セットアップ ツール
Windows インストーラ パッケージの開発環境には、さまざまなサードパーティ製のセットアップ ツールが用意されています。 以下の無料ツールを利用できます。

- インストールシールド限定版

   Visual Studio の **[新しいプロジェクト**] ダイアログ ボックスでは、インストール シールドの限定バージョンを取得できます。 **[その他のプロジェクトの種類]** を展開し、[**セットアップと配置**] を選択します。 インストールシールドテンプレートを選択します。

- Windows インストーラ XML ツールセット

   Windows インストーラ XML (WiX) ツールセットは、XML ソース ファイルから Windows インストーラ パッケージをビルドします。 WiX ツールセットは、マイクロソフトのオープン ソース プロジェクトです。 ソース コードと実行可能ファイルは[、Wix ツールセット](https://sourceforge.net/projects/wix/)からダウンロードできます。

   を使用して に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合する商用製品については、「 [Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)」を参照してください。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]

## <a name="see-also"></a>関連項目
- [Windows インストーラーを使用して VS パッケージをインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
