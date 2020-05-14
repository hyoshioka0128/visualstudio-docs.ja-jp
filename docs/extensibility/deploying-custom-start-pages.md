---
title: カスタムスタートページの展開 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 210b4589c0e2165af537c3fa9129affb06197e9b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712225"
---
# <a name="deploy-custom-start-pages"></a>カスタムスタート ページの展開

カスタム スタート ページを配置するには、VSIX 配置を使用するか、ターゲット コンピューター上の適切な場所にファイルをコピーします。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>スタート ページ プロジェクト テンプレートを使用した VSIX 配置

スタート ページ プロジェクト テンプレートを使用してスタート ページを作成し、プロジェクトをビルドすると、配布できる *.vsix*ファイルが作成されます。 スタート ページを *.vsix*ファイルにパッケージ化すると、対象ユーザーに応じて、次の展開オプションが提供されます。

- *.vsix*ファイルは、ネットワーク共有またはパブリック Web サイトに配置できます。 ファイルを開くと、スタート ページが自動的にインストールされます。

- *.vsix*ファイルを[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)Web サイトにアップロードすると、ユーザーは**拡張機能マネージャー**を使用してインストールできます。

スタート ページ プロジェクト テンプレートは、既定の Visual Studio スタート ページのコピーを作成し、コピーを変更して元のページを保持できるようにします。

スタート ページ プロジェクト テンプレートは **、拡張機能マネージャー**を使用するか、Web サイトからダウンロードして取得できます。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>スタート ページ プロジェクト テンプレートを使用しない VSIX 配置
 VSIX の展開が成功するには、VSIX 登録プロセスと**拡張機能マネージャー**によって認識されるフォルダーに拡張機能をインストールする必要があります。 スタート ページ プロジェクト テンプレートは既に正しいフォルダーを指定しているため、VSIX 展開用の拡張機能をパッケージ化する場合は常に使用することをお勧めします。 ただし、テンプレートを使用できない場合は、VSIX 配置を使用せずに作成できます。

 スタート ページ プロジェクト テンプレートを使用せずに VSIX 配置を作成するには、次の 2 つの方法のいずれかでスタート ページの *.vsix*ファイルを作成します。

- 空の VSIX プロジェクトにカスタム スタート ページ ファイルを追加します。 詳細については[、「VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

- *.vsix*ファイルを手動で作成する。 *vsix*ファイルを手動で作成するには、次の手順を実行します。

   1. 新しいフォルダーに*拡張子.vsixmanifest*ファイルと *[Content_Types].xml*ファイルを作成します。 詳細については、「 [VSIX パッケージの解剖学](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

   2. エクスプローラで、2 つの XML ファイルが含まれているフォルダを右クリックし、[**送信**] をクリックします。 生成された *.zip*ファイルの名前を*Filename.vsix*に変更します。

Visual Studio がスタート ページを認識`Content Element`するには、VSIX マニフェストの`CustomExtension Element`に、属性`Type`が に`"StartPage"`設定された が含まれている必要があります。 VSIX 配置を使用してインストールされたスタート ページ拡張機能が、[**スタートアップ**オプション] ページの [**スタート ページのカスタマイズ**] リストに **[インストールされた拡張機能]** *拡張子として*表示されます。

スタート ページ パッケージにアセンブリが含まれている場合は、Visual Studio の起動時に使用できるように、バインド パス登録を追加する必要があります。 これを行うには、パッケージに次の情報を含む *.pkgdef*ファイルが含まれていることを確認します。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>すべてのユーザーに対する VSIX 展開
 既定では、VSIX パッケージに配置された拡張機能は、現在のユーザーに対してのみインストールされます。 すべてのユーザーの展開を作成することで、ターゲット マシンのすべてのユーザーに対してスタート ページのインストールを行うことができます。

### <a name="to-create-an-all-users-deployment"></a>全ユーザー展開を作成するには

1. コード ビューで*拡張子.vsixmanifest*ファイルを開きます。

2. vsix`Identifier`マニフェストの要素に、値が`AllUsers``true`を持つ要素を追加します。

    ```
    <AllUsers>true</AllUsers>
    ```

     これにより、vsix インストーラは管理者のアクセス許可を要求し *、\Common7\IDE\拡張機能*にファイルをインストールします。

3. *pkgdef*ファイルを開きます。

4. *次*の例を追加して、HKLM の下の既定の開始ページを設定する *.pkgdef*を変更します。 *.xaml*

     [$RootKey$\スタートページ\デフォルト]

     "Uri"="$PackageFolder$\\*MyStartPage.xaml*"

     これにより、新しいスタート ページの場所を見るように Visual Studio に指示します。

## <a name="file-copy-deployment"></a>ファイル コピーの配置
 カスタム スタート ページを展開するために *.vsix*ファイルを作成する必要はありません。 代わりに、マークアップとサポート ファイルをユーザーの<em>\StartPages\*フォルダに直接コピーできます。*Customize Start Page</em> [* **スタートアップ**オプション ] ページの [ * スタート ページのカスタマイズ ] リストには、そのフォルダー内のすべての *.xaml*ファイルがパスと共に一覧表示*されます。\\* スタート ページにプライベート アセンブリへの参照が含まれている場合は、それらをコピーして *\PrivateAssemblyies\*フォルダーに貼り付ける必要があります。

 *.vsix*ファイルにパッケージ化せずに作成したスタート ページを配布するには、バッチ スクリプトなどの基本的なファイル コピー戦略を使用して、必要なディレクトリにファイルを配置することをお勧めします。

### <a name="to-manually-install-a-custom-start-page"></a>カスタムスタートページを手動でインストールするには

1. スタート ページマークアップを含む *.xaml*ファイルをアセンブリ以外のサポート ファイルと共にコピーし、ユーザーの *\StartPages\*フォルダーに貼り付けます。

2. スタート ページにアセンブリが必要な場合は、アセンブリをコピーして *..{Visual Studio のインストール フォルダー}\コモン7\IDE\プライベート アセンブリ\\。 \\*

3. [**スタートアップ**オプション] ページの [**スタート ページのカスタマイズ**] リストで、新しいスタート ページを選択します。 詳細については、「[スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)
- [スタート ページにユーザー コントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
