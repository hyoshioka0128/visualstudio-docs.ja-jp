---
title: Windows インストーラーパッケージを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 58529dabbb52ceb751c67be24beb1d21285a1de6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301133"
---
# <a name="authoring-a-windows-installer-package"></a>Windows インストーラー パッケージの編集
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

データは Windows インストーラーモデルを駆動します。 たとえば、ファイルをコピーしてレジストリエントリを書き込むための手続き型スクリプトを記述するのではなく、ファイルとレジストリデータを格納するデータベーステーブルの行と列を作成します。  
  
## <a name="database-entries"></a>[データベース エントリ]  
 VSPackage をインストールするには、Windows インストーラーパッケージに次のタスクを実行するためのデータベースエントリが含まれている必要があります。  
  
- システムを検索して、VSPackage がサポートしている [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のバージョンを探します (AppSearch、CompLocator、RegLocator、DrLocator、署名を含むテーブル Windows インストーラーを使用します)。  
  
- サポートされているバージョンの [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] がインストールされていない場合、または VSPackage の別のシステム要件 (LaunchCondition テーブルを使用) が満たされていない場合は、インストールをキャンセルします。  
  
- ディレクトリ、コンポーネント、およびファイルテーブルを使用して、VSPackage ファイルと依存ファイルをインストールします。  
  
- VSPackage の適切な情報をレジストリに追加します (レジストリテーブルを使用します)。  
  
- **Devenv.exe/セットアップ**を呼び出して (CustomAction テーブルを使用して) [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の VSPackage を統合します。  
  
  詳細については、「 [Windows インストーラー](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)」を参照してください。  
  
## <a name="setup-tools"></a>セットアップツール  
 さまざまなサードパーティ製セットアップツールは、Windows インストーラーパッケージの開発環境を提供します。 次の2つの無料ツールがあります。  
  
- InstallShield Limited Edition  
  
   Visual Studio の **[新しいプロジェクト]** ダイアログボックスでは、InstallShield の限定バージョンを取得できます。 **[その他のプロジェクトの種類]** を展開し、 **[セットアップと配置]** を選択します。 InstallShield テンプレートを選択します。  
  
- Windows Installer XML Toolset  
  
   ツールセットは、XML ソースファイルから Windows インストーラーパッケージをビルドします。 ツールセットは、Microsoft オープンソースプロジェクトです。 ソースコードと実行可能ファイルは[http://sourceforge.net/projects/wix](https://sourceforge.net/projects/wix/)からダウンロードできます。  
  
  [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]を使用して [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] に統合される商用製品の場合は、「 [https://marketplace.visualstudio.com/](https://marketplace.visualstudio.com/)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
