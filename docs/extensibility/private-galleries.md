---
title: プライベートギャラリー |Microsoft Docs
description: Visual Studio SDK で開発したコントロール、テンプレート、ツールをプライベートギャラリーに投稿することによって共有する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1ec7390acf753af20bc0edbe20194ba17c2d9d80
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863499"
---
# <a name="private-galleries"></a>プライベート ギャラリー
次のように、組織のイントラネット上の *プライベートギャラリー* に投稿することで、開発したコントロール、テンプレート、およびツールを共有できます。

- イントラネット上の適切に構成された中央の場所 (リポジトリ) に Atom (RSS) フィードを作成します。 詳細については、「 [方法: プライベートギャラリーの Atom フィードを作成](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)する」を参照してください。

- プライベートギャラリーを説明する、 *pkgdef* ファイルを配布します。 この構成は、プライベートギャラリーを多数のコンピューターに同時に接続する管理者にお勧めします。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>Visual Studio の拡張機能と更新プログラムにプライベートギャラリーを追加する
 プライベートギャラリーが使用可能な場合は、Visual Studio の **拡張機能と更新プログラム** に追加できます。

 ![拡張機能マネージャーの追加ダイアログ](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>拡張機能と更新プログラムにプライベートギャラリーを追加するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

2. [ **環境** ] ノードで、[ **拡張機能と更新プログラム**] を選択します。

3. **[追加]** ボタンを選びます。

4. [ **名前** ] フィールドに、プライベートギャラリーの名前 (など) を入力し `My Gallery` ます。

5. [ **Url** ] フィールドに、プライベートギャラリーをホストしている Atom フィードまたは SharePoint サイトの url を入力します。

    1. ホストがプライベートギャラリーに接続する Atom フィードである場合、URL はのようになり `http://www.mywebsite/mygallery/atom.xml` ます。  この URL は、ファイルまたはネットワークパスを参照できます。

    2. ホストが SharePoint サイトの場合、URL はのようになり `http://mysharepoint/sites/mygallery/forms/AllItems.aspx` ます。

### <a name="manage-private-galleries"></a>プライベートギャラリーの管理
 管理者は、各コンピューターのシステムレジストリを変更することで、複数のコンピューターで同時にプライベートギャラリーを使用できるようにすることができます。 これを実現するには、新しいレジストリキーとその値を記述する、 *pkgdef* ファイルを作成します。  このファイルの形式は次のとおりです。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 詳細については、「 [方法: レジストリ設定を使用してプライベートギャラリーを管理](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)する」を参照してください。

## <a name="install-extensions-from-a-private-gallery"></a>プライベートギャラリーから拡張機能をインストールする
 **拡張機能と更新プログラム** で、プライベートギャラリーから Visual Studio 拡張機能を検索してインストールすることができます。 次の手順では、という名前のプライベートギャラリーを使用し `My Gallery` ます。

 ![プライベート ギャラリーをインストールする拡張機能マネージャー](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>プライベートギャラリーから拡張機能を検索してインストールするには

1. メニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

2. 左側のウィンドウで、[ **オンライン拡張**] を選択し、[ **マイギャラリー**] を選択します。

3. 右側のウィンドウで、拡張機能を選択し、[ **ダウンロード** ] ボタンを選択します。

## <a name="update-extensions-from-a-private-gallery"></a>プライベートギャラリーから拡張機能を更新する
 新しいバージョンの Visual Studio 拡張機能がプライベートギャラリーに投稿されると、インストールされている拡張機能を更新できます。 次の手順では、という名前のプライベートギャラリーを使用し `My Repository` ます。

 ![拡張機能マネージャーのプライベート ギャラリーの更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>インストールされている拡張機能をプライベートギャラリーから更新するには

1. メニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

2. 左側のウィンドウで、[ **更新プログラム**] を選択し、[ **マイリポジトリ**] を選択します。

3. 右側のウィンドウで、拡張機能を選択し、[ **更新** ] ボタンをクリックします。

## <a name="see-also"></a>関連項目
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
- [Visual Studio 拡張機能を出荷する](../extensibility/shipping-visual-studio-extensions.md)
