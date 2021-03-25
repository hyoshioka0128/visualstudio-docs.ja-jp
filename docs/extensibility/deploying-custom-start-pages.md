---
title: カスタムスタートページの配置 |Microsoft Docs
description: VSIX 配置を使用するか、ターゲットコンピューター上の正しい場所にファイルをコピーして、カスタムスタートページを展開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: a356fe3dadaf0eca4f0b4d0f2a7d17f0b475acfb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061408"
---
# <a name="deploy-custom-start-pages"></a>カスタムスタートページのデプロイ

VSIX 配置を使用するか、ターゲットコンピューター上の正しい場所にファイルをコピーすることで、カスタムスタートページを配置できます。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>スタートページのプロジェクトテンプレートを使用した VSIX 配置

スタートページのプロジェクトテンプレートを使用してスタートページを作成し、プロジェクトをビルドすると、Visual Studio によって、配布できる *.vsix* ファイルが作成されます。 *.Vsix* ファイルにスタートページをパッケージ化すると、対象ユーザーに応じて次の配置オプションを使用できます。

- *.Vsix* ファイルは、ネットワーク共有またはパブリック Web サイトに配置できます。 他のユーザーがファイルを開くと、スタートページが自動的にインストールされます。

- *.Vsix* ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードして、ユーザーが **拡張機能マネージャー** を使用してインストールできるようにすることができます。

スタートページのプロジェクトテンプレートによって、既定の Visual Studio のスタートページのコピーが作成されます。これにより、コピーを変更して元のファイルを保持することができます。

スタートページのプロジェクトテンプレートを取得するには、 **拡張機能マネージャー** を使用するか、Web サイトからダウンロードします。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>スタートページのプロジェクトテンプレートを使用しない VSIX 配置
 VSIX 配置を正常に実行するには、VSIX 登録プロセスおよび **拡張機能マネージャー** によって認識されるフォルダーに拡張機能をインストールする必要があります。 スタートページのプロジェクトテンプレートには既に正しいフォルダーが指定されているので、VSIX 配置用の拡張機能をパッケージ化する場合は、このテンプレートを使用することをお勧めします。 ただし、テンプレートを使用できない場合は、VSIX の配置を使用せずに作成できます。

 スタートページのプロジェクトテンプレートを使用せずに VSIX の配置を作成するには、最初に次の2つの方法のいずれかで、スタートページの *.vsix* ファイルを作成します。

- カスタムスタートページファイルを空の VSIX プロジェクトに追加する。 詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

- *.Vsix* ファイルを手動で作成する。 .Vsix ファイルを手動で作成するには、次のように *します* 。

   1. 新しいフォルダーに *source.extension.vsixmanifest* ファイルと *[Content_Types] .xml* ファイルを作成します。 詳細については、「 [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

   2. Windows エクスプローラーで、2つの XML ファイルが含まれているフォルダーを右クリックし、[ **送信**] をクリックして、[圧縮 (zip 形式) フォルダー] をクリックします。 結果の *.zip* ファイルの名前を *filename .vsix* に変更します。ここで、filename はパッケージをインストールする再頒布可能ファイルの名前です。

Visual Studio がスタートページを認識するには、 `Content Element` VSIX マニフェストのに、属性がに設定されたが含まれている必要があり `CustomExtension Element` `Type` `"StartPage"` ます。 VSIX 配置を使用してインストールされたスタートページの拡張機能は、[**スタートアップ** オプション] ページの [**スタートページのカスタマイズ**] の一覧に [インストールされて **いる拡張機能]** の *名前* として表示されます。

スタートページパッケージにアセンブリが含まれている場合は、Visual Studio の起動時に使用できるように、バインドパス登録を追加する必要があります。 これを行うには、パッケージに次の情報を含む *pkgdef* ファイルが含まれていることを確認してください。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>すべてのユーザーの VSIX 配置
 既定では、VSIX パッケージに配置された拡張機能は、現在のユーザーに対してのみインストールされます。 All-Users の展開を作成することによって、ターゲットコンピューターのすべてのユーザーに対してスタートページのインストールを行うことができます。

### <a name="to-create-an-all-users-deployment"></a>All-Users の展開を作成するには

1. コードビューで *source.extension.vsixmanifest* ファイルを開きます。

2. `Identifier`Vsix マニフェストの要素に、 `AllUsers` の値を持つ要素を追加し `true` ます。

    ```
    <AllUsers>true</AllUsers>
    ```

     これにより、vsix インストーラーによって管理者のアクセス許可が求められ、 *\Common7\IDE\Extensions* にファイルがインストールされます。

3. *Pkgdef* ファイルを開きます。

4. 次のように追加して、[HKLM] の下に既定のスタートページを設定するように *pkgdef* を変更します。ここで、 *Mystartpage* は、スタートページを含む *.xaml* ファイルの名前です。

     [$RootKey $ \ Startpage\ 既定値]

     "Uri" = "$PackageFolder $ \\ *mystartpage. .xaml*"

     これにより、Visual Studio に新しいスタートページの場所を検索するように指示されます。

## <a name="file-copy-deployment"></a>ファイルコピーの展開
 カスタムスタートページを配置するための *.vsix* ファイルを作成する必要はありません。 代わりに、マークアップとサポートファイルをユーザーの \ startpages フォルダーに直接コピーすることができ <em> \* ます。*</em>* [**スタートアップ** オプション] ページの [スタートページのカスタマイズ] の一覧には、そのフォルダー内のすべての *.xaml* ファイルとパス (たとえば、 *%USERPROFILE%\My Documents\Visual Studio {version} \ startpages \\ {file Name} .xaml*) が表示されます。 スタートページにプライベートアセンブリへの参照が含まれている場合は、それらをコピーして、* \ privateassemblies フォルダーに貼り付ける必要があり \* ます。

 作成したスタートページを *.vsix* ファイルにパッケージ化せずに配布するには、基本的なファイルコピー方法 (バッチスクリプトなど)、または必要なディレクトリにファイルを配置するその他の展開テクノロジを使用することをお勧めします。

### <a name="to-manually-install-a-custom-start-page"></a>カスタムスタートページを手動でインストールするには

1. スタートページのマークアップを含む *.xaml* ファイルを、アセンブリ以外のサポートファイルと共にコピーし、ユーザーの * \ startpages フォルダーに貼り付けます。 \*

2. スタートページにアセンブリが必要な場合は、それをコピーし、に貼り付けます。 *\\{Visual Studio インストールフォルダー} \Common7\IDE\PrivateAssemblies \\*。

3. [**スタートアップ** オプション] ページの [**スタートページのカスタマイズ**] の一覧で、新しいスタートページを選択します。 詳細については、「 [スタートページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [スタートページをカスタマイズする](../ide/customizing-the-start-page-for-visual-studio.md)
- [スタートページにユーザーコントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
