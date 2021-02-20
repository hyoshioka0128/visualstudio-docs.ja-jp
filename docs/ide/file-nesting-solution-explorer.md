---
title: ソリューション エクスプローラーでのファイルの入れ子のルール
description: ソリューション エクスプローラーでのファイルの入れ子のルール、プリセット、およびカスタマイズについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/25/2018
ms.topic: conceptual
helpviewer_keywords:
- file nesting
- Solution Explorer, file nesting
author: angelosp
ms.author: angelpe
manager: jmartens
ms.openlocfilehash: aa3ca640fed4e32c19defd925a49369890219035
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99869454"
---
# <a name="file-nesting-in-solution-explorer"></a>ソリューション エクスプローラーでのファイルの入れ子

**ソリューション エクスプローラー** では、関連ファイルを入れ子にして、それらを整理し、見つけやすくしています。 たとえば、Windows Forms フォームをプロジェクトに追加すると、**ソリューション エクスプローラー** で、フォームの下にフォームのコード ファイルが入れ子にされます。 ASP.NET Core プロジェクトでは、ファイルの入れ子をさらに一歩進めることができます。 ファイルの入れ子のプリセットの **[オフ]**、**[既定]**、**[Web]** から選択できます。 さらに、[ファイルの入れ子の方法をカスタマイズ](#customize-file-nesting)したり、[ソリューション固有およびプロジェクト固有の設定を作成](#create-project-specific-settings)したりすることもできます。

> [!NOTE]
> 現在、この機能は ASP.NET Core プロジェクトでのみサポートされています。

## <a name="file-nesting-options"></a>ファイルの入れ子のオプション

![ファイルの入れ子をオン/オフにするボタン](media/filenesting_onoff.png)

カスタマイズせずに使用できるファイルの入れ子のオプションは次のとおりです。

* **[オフ]**: 何も入れ子にせず、ファイルの単純なリストが作成されます。

* **[既定]**: このオプションは、**ソリューション エクスプローラー** での既定のファイル入れ子動作を提供します。 特定のプロジェクト タイプに設定が存在しない場合、そのプロジェクトのファイルは入れ子になりません。 Web プロジェクトのように設定が存在する場合は、入れ子が適用されます。

* **[Web]**: **Web** ファイルの入れ子動作を、現在のソリューションのすべてのプロジェクトに適用します。 多くのルールがあるので、是非ご確認いただき、ご意見をお聞かせください。 次のスクリーンショットでは、このオプションを指定したときのファイル入れ子動作のいくつかの例を示します。

   ![ソリューション エクスプローラーでのファイルの入れ子](media/filenesting.png)

## <a name="customize-file-nesting"></a>ファイルの入れ子をカスタマイズする

既定の動作が適切ではない場合は、ファイルを入れ子にする方法を **ソリューション エクスプローラー** に指示する、独自のカスタム ファイル入れ子設定を作成できます。 必要なだけいくつでもカスタム ファイル入れ子設定を追加でき、必要に応じてそれらを切り替えることができます。 新しいカスタム設定を作成するには、空のファイルから始めるか、または **Web** の設定を基にすることができます。

![カスタム ファイル入れ子ルールを追加する](media/filenesting_addcustom.png)

既に機能するものを使って作業する方が簡単なので、**Web** の設定を基にすることをお勧めします。 **Web** の設定を基にする場合、*.filenesting.json* ファイルは次のようになります。

![既存のファイル入れ子ルールをカスタム設定の基にする](media/filenesting_editcustom.png)

ノード **dependentFileProviders** とその子ノードに注目してください。 各子ノードは、Visual Studio がファイルを入れ子にするために使用できるルールの種類です。 たとえば、**ファイル名は同じにして、拡張子は異なるものにする**、というのはルールの 1 つの種類です。 使用できるルールは次のとおりです。

* **extensionToExtension**: *file.js* を *file.ts* の下に入れ子にするには、このルールの種類を使います

* **fileSuffixToExtension**: *file-vsdoc.js* を *file.js* の下に入れ子にするには、このルールの種類を使います

* **addedExtension**: *file.html.css* を *file.html* の下に入れ子にするには、このルールの種類を使います

* **pathSegment**: *jquery.min.js* を *jquery.js* の下に入れ子にするには、このルールの種類を使います

* **allExtensions**: *file.** を *file.js* の下に入れ子にするには、このルールの種類を使います

* **fileToFile**: *bower.json* を *.bowerrc* の下に入れ子にするには、このルールの種類を使います

### <a name="the-extensiontoextension-provider"></a>extensionToExtension プロバイダー

このプロバイダーでは、特定のファイル拡張子を使ってファイル入れ子ルールを定義できます。 次の例を確認してください。

![extentionToExtension ルールの例](media/filenesting_extensiontoextension.png) ![extentionToExtension の効果の例](media/filenesting_extensiontoextension_effect.png)

* 1 番目の **extensionToExtension** ルールのため、*cart.js* は *cart.ts* の下の入れ子になります。

* *cart.js* は *cart.tsx* の下の入れ子にはなりません。これは、ルールで **.ts** は **.tsx** より前にあり、親になることができるのは 1 つだけであるためです。

* 2 番目の **extensionToExtension** ルールのため、*light.css* は *light.sass* の下の入れ子になります。

* 3 番目の **extensionToExtension** ルールのため、*home.html* は *home.md* の下の入れ子になります。

### <a name="the-filesuffixtoextension-provider"></a>fileSuffixToExtension プロバイダー

このプロバイダーは **extensionToExtension** と同じように動作しますが、唯一の違いは、ルールが拡張子だけでなくファイルのサフィックスも確認することです。 次の例を確認してください。

![fileSuffixToExtension ルールの例](media/filenesting_filesuffixtoextension.png) ![fileSuffixToExtension の効果の例](media/filenesting_filesuffixtoextension_effect.png)

* **fileSuffixToExtension** ルールのため、*portal-vsdoc.js* は *portal.js* の下の入れ子になります。

* ルールの他の部分はすべて、**extensionToExtension** と同じように機能します

### <a name="the-addedextension-provider"></a>addedExtension プロバイダー

このプロバイダーは、追加の拡張子があるファイルを、追加の拡張子がないファイルの下に入れ子にします。 追加の拡張子は、完全なファイル名の末尾にのみ使用できます。

次の例を確認してください。

![addedExtension ルールの例](media/filenesting_addedextension.png) ![addedExtension の効果の例](media/filenesting_addedextension_effect.png)

* **addedExtension** ルールのため、*file.html.css* は *file.html* の下の入れ子になります。

> [!NOTE]
> `addedExtension` ルールに対してファイル拡張子は何も指定しません。すべてのファイル拡張子に自動的に適用されます。 つまり、別のファイルと同じ名前と拡張子を持ち、その最後に拡張子が追加されているすべてのファイルは、他のファイルの下に入れ子にされます。 このプロバイダーの効果を特定のファイル拡張子だけに制限することはできません。

### <a name="the-pathsegment-provider"></a>pathSegment プロバイダー

このプロバイダーは、追加の拡張子があるファイルを、追加の拡張子がないファイルの下に入れ子にします。 追加の拡張子は、完全なファイル名の中間にのみ使用できます。

次の例を確認してください。

![pathSegment ルールの例](media/filenesting_pathsegment.png) ![pathSegment の効果の例](media/filenesting_pathsegment_effect.png)

* **pathSegment** ルールのため、*jquery.min.js* は *jquery.js* の下の入れ子になります。

> [!NOTE]
> - `pathSegment` ルールに対して特定のファイル拡張子を指定しないと、すべてのファイル拡張子に適用されます。 つまり、別のファイルと同じ名前と拡張子を持ち、その途中に拡張子が追加されているすべてのファイルは、他のファイルの下に入れ子にされます。
> - 次の方法で指定することにより、`pathSegment` ルールの効果を特定のファイル拡張子に制限することができます。
>
>    ```json
>    "pathSegment": {
>       "add": {
>         ".*": [
>           ".js",
>           ".css",
>           ".html",
>           ".htm"
>         ]
>       }
>    }
>    ```

### <a name="the-allextensions-provider"></a>allExtensions プロバイダー

このプロバイダーを使うと、基本のファイル名が同じで任意の拡張子を持つファイルのファイル入れ子ルールを定義できます。 次の例を確認してください。

![allExtensions ルールの例](media/filenesting_allextensions.png) ![allExtensions の効果の例](media/filenesting_allextensions_effect.png)

* **allExtensions** ルールのため、*template.cs* と *template.doc* は *template.tt* の下の入れ子になります。

### <a name="the-filetofile-provider"></a>fileToFile プロバイダー

このプロバイダーでは、ファイル名全体に基づくファイル入れ子ルールを定義できます。 次の例を確認してください。

![fileToFile ルールの例](media/filenesting_filetofile.png) ![fileToFile の効果の例](media/filenesting_filetofile_effect.png)

* **fileToFile** ルールのため、*.bowerrc* は *bower.json* の下の入れ子になります。

### <a name="rule-order"></a>ルールの順序

順序は、カスタム設定ファイルのすべての部分において重要です。 **dependentFileProvider** ノードの内部で上または下に移動することにより、ルールの実行順序を変更できます。 たとえば、あるルールでは **file.js** を **file.ts** の親にするようにしていて、別のルールでは **file.coffee** を **file.ts** の親にするようにしている場合、ファイルでのルールの出現順序は、3 つのファイルがすべて存在する場合の入れ子動作を示します。 **file.ts** が持つことのできる親は 1 つだけなので、最初に実行されるルールが適用されます。

セクション内のファイルの順序だけでなく、ルール セクション自体の順序も重要です。 ファイルのペアがファイル入れ子ルールに一致するとすぐ、ファイル内でそれより下にある他のルールは無視され、次のファイル ペアが処理されます。

### <a name="file-nesting-button"></a>ファイル入れ子ボタン

独自のカスタム設定を含むすべての設定を、**ソリューション エクスプローラー** の同じボタンを使って管理できます。

![カスタム ファイル入れ子ルールをアクティブにする](media/filenesting_activatecustom.png)

## <a name="create-project-specific-settings"></a>プロジェクト固有の設定を作成する

各ソリューションとプロジェクトの右クリック メニュー (コンテキスト メニュー) から、ソリューション固有およびプロジェクト固有の設定を作成できます。

![ソリューション固有およびプロジェクト固有の入れ子ルール](media/filenesting_solutionprojectspecific.png)

ソリューション固有およびプロジェクト固有の設定は、Visual Studio のアクティブな設定と結合されます。 たとえば、プロジェクト固有の設定ファイルを空にしても、**ソリューション エクスプローラー** はファイルを入れ子にします。 入れ子の動作は、ソリューション固有の設定または Visual Studio の設定のいずれかが使われます。 ファイル入れ子設定をマージするときの優先順位は、Visual Studio > ソリューション > プロジェクトです。

**[ツール]** > **[オプション]** > **[ASP.NET Core]** > **[ファイルの入れ子]** で **[ソリューションおよびプロジェクトの設定を無視する]** オプションを有効にすることにより、ディスク上にファイルが存在する場合であってもソリューション固有およびプロジェクト固有の設定を無視するよう、Visual Studio に指示できます。

また、その逆も可能で、**root** ノードを **true** に設定することにより、ソリューション固有またはプロジェクト固有の設定 "*だけ*" を使うよう、Visual Studio に指示できます。 Visual Studio はそのレベルでのファイルのマージを停止し、階層でそれより上位にあるファイルと結合しません。

ソリューション固有およびプロジェクト固有の設定をソース管理にチェックインすることができ、コードベースで作業するチーム全体がその設定を共有できます。

## <a name="disable-file-nesting-rules-for-a-project"></a>プロジェクトのファイルの入れ子ルールを無効にする

プロバイダーで **add** の代わりに **remove** アクションを使うことで、特定のソリューションまたはプロジェクトの既存のグローバル ファイル入れ子ルールを無効にすることができます。 たとえば、次の設定コードをプロジェクトに追加した場合、この特定のプロジェクトに対してグローバルに存在する可能性があるすべての **pathSegment** ルールは無効になります。

```json
"dependentFileProviders": {
  "remove": {
    "pathSegment": {}
  }
}
```

## <a name="see-also"></a>関連項目

- [IDE をカスタマイズする](../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio のソリューションおよびプロジェクト](solutions-and-projects-in-visual-studio.md)
