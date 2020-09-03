---
title: カスタムスタートページの配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1cdd172c2960024da8b12735764161d36498c4e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162106"
---
# <a name="deploying-custom-start-pages"></a>カスタム スタート ページのデプロイ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSIX 配置を使用するか、ターゲットコンピューター上の正しい場所にファイルをコピーすることで、カスタムスタートページを配置できます。  
  
## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>スタートページのプロジェクトテンプレートを使用した VSIX 配置  
 スタートページのプロジェクトテンプレートを使用してスタートページを作成し、プロジェクトをビルドすると、Visual Studio によって、配布できる .vsix ファイルが作成されます。 .Vsix ファイルにスタートページをパッケージ化すると、対象ユーザーに応じて次の配置オプションを使用できます。  
  
- .Vsix ファイルは、ネットワーク共有またはパブリック Web サイトに配置できます。 他のユーザーがファイルを開くと、スタートページが自動的にインストールされます。  
  
- .Vsix ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードして、ユーザーが **拡張機能マネージャー**を使用してインストールできるようにすることができます。  
  
  スタートページのプロジェクトテンプレートによって、既定の Visual Studio のスタートページのコピーが作成されます。これにより、コピーを変更して元のファイルを保持することができます。  
  
  スタートページのプロジェクトテンプレートを取得するには、 **拡張機能マネージャー** を使用するか、Web サイトからダウンロードします。  
  
## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>スタートページのプロジェクトテンプレートを使用しない VSIX 配置  
 VSIX 配置を正常に実行するには、VSIX 登録プロセスおよび **拡張機能マネージャー**によって認識されるフォルダーに拡張機能をインストールする必要があります。 スタートページのプロジェクトテンプレートには既に正しいフォルダーが指定されているので、VSIX 配置用の拡張機能をパッケージ化する場合は、このテンプレートを使用することをお勧めします。 ただし、テンプレートを使用できない場合は、VSIX の配置を使用せずに作成できます。  
  
 スタートページのプロジェクトテンプレートを使用せずに VSIX の配置を作成するには、最初に次の2つの方法のいずれかで、スタートページの .vsix ファイルを作成します。  
  
- カスタムスタートページファイルを空の VSIX プロジェクトに追加する。 詳細については、「 [VSIX プロジェクトテンプレート](../extensibility/vsix-project-template.md)」を参照してください。  
  
- .Vsix ファイルを手動で作成する。 詳細については、「 [方法: 拡張機能を手動でパッケージ化する (VSIX 配置)](../misc/how-to-manually-package-an-extension-vsix-deployment.md)」を参照してください。  
  
  Visual Studio がスタートページを認識するには、 `Content Element` VSIX マニフェストのに、属性がに設定されたが含まれている必要があり `CustomExtension Element` `Type` `"StartPage"` ます。 VSIX 配置を使用してインストールされたスタートページの拡張機能は、[**スタートアップ**オプション] ページの [**スタートページのカスタマイズ**] の一覧に [インストールされて**いる拡張機能]** の*名前*として表示されます。  
  
  スタートページパッケージにアセンブリが含まれている場合は、Visual Studio の起動時に使用できるように、バインドパス登録を追加する必要があります。 これを行うには、パッケージに次の情報を含む pkgdef ファイルが含まれていることを確認してください。  
  
```  
[$RootKey$\BindingPaths\{Insert a new GUID here}]  
"$PackageFolder$"=""  
```  
  
### <a name="vsix-deployment-for-all-users"></a>すべてのユーザーの VSIX 配置  
 既定では、VSIX パッケージに配置された拡張機能は、現在のユーザーに対してのみインストールされます。 すべてのユーザーの展開を作成することによって、ターゲットコンピューターのすべてのユーザーに対してスタートページのインストールを行うことができます。  
  
##### <a name="to-create-an-all-users-deployment"></a>すべてのユーザーの展開を作成するには  
  
1. コードビューで source.extension.vsixmanifest ファイルを開きます。  
  
2. `Identifier`Vsix マニフェストの要素に、 `AllUsers` の値を持つ要素を追加し `true` ます。  
  
    ```  
    <AllUsers>true</AllUsers>  
    ```  
  
     これにより、vsix インストーラーによって管理者のアクセス許可が求められ、\Common7\IDE\Extensions. にファイルがインストールされます。  
  
3. Pkgdef ファイルを開きます。  
  
4. 次のように追加して、[HKLM] の下に既定のスタートページを設定するように pkgdef を変更します。ここで、 *Mystartpage* は、スタートページを含む .xaml ファイルの名前です。  
  
     [$RootKey $ \ Startpage\ 既定値]  
  
     "Uri" = "$PackageFolder $ \\ *mystartpage. .xaml*"  
  
     これにより、新しいスタートページの場所を検索するように Visual そこに指示されます。  
  
## <a name="file-copy-deployment"></a>ファイルコピーの展開  
 カスタムスタートページを配置するための .vsix ファイルを作成する必要はありません。 代わりに、マークアップとサポートファイルをユーザーの \ スタート \ フォルダーに直接コピーすることができます。 **スタートアップ**オプションページの [**スタートページのカスタマイズ**] の一覧には、そのフォルダー内のすべての .xaml ファイルがパスと共に表示されます (たとえば、%USERPROFILE%\My Documents\Visual Studio*バージョン*\ startpages \\ *ファイル名*.xaml)。 スタートページにプライベートアセンブリへの参照が含まれている場合は、それらをコピーして、\PrivateAssemblies\ フォルダーに貼り付ける必要があります。  
  
 作成したスタートページを .vsix ファイルにパッケージ化せずに配布するには、基本的なファイルコピー方法 (バッチスクリプトなど)、または必要なディレクトリにファイルを配置するその他の展開テクノロジを使用することをお勧めします。  
  
#### <a name="to-manually-install-a-custom-start-page"></a>カスタムスタートページを手動でインストールするには  
  
1. スタートページのマークアップを含む .xaml ファイルを、アセンブリ以外のサポートファイルと共にコピーし、ユーザーの \ スタートページ \ フォルダーに貼り付けます。  
  
2. スタートページにアセンブリが必要な場合は、それをコピーし、に貼り付けます \\ 。*Visual Studio のインストールフォルダー*\Common7\IDE\PrivateAssemblies \\ 。  
  
3. [**スタートアップ**オプション] ページの [**スタートページのカスタマイズ**] の一覧で、新しいスタートページを選択します。 詳細については、[スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [スタートページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)   
 [スタート ページへのユーザー コントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)
