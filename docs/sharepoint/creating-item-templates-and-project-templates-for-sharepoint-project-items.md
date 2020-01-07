---
title: SharePoint プロジェクト項目の項目テンプレート/プロジェクトテンプレート
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- .spdata files
- projects [SharePoint development in Visual Studio], creating custom templates
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, creating custom project and item templates
- project items [SharePoint development in Visual Studio], creating custom templates
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65bbd58bf9b3e0b399603a083615daccc382a98f
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981174"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する

カスタム SharePoint プロジェクト項目の種類を定義すると、それを項目テンプレートまたはプロジェクトテンプレートに関連付けることができます。 この関連付けにより、他の開発者は Visual Studio でプロジェクト項目を使用できるようになります。 テンプレートのウィザードを作成することもできます。

たとえば、Visual Studio には、SharePoint サイトにフィールドを追加するためのプロジェクトテンプレートまたは項目テンプレートは含まれていません。 フィールドを表す SharePoint プロジェクト項目の種類を定義し、他の開発者がフィールド項目を SharePoint プロジェクトに追加するために使用できる項目テンプレートを作成できます。 または、プロジェクトテンプレートを構築して、開発者がフィールド項目を含む新しい SharePoint プロジェクトを作成できるようにすることもできます。 どちらの場合も、開発者がテンプレートを使用するときに表示されるウィザードを提供できます。 このウィザードでは、開発者からの情報を収集して、新しい項目またはプロジェクトを構成できます。

項目テンプレートとプロジェクトテンプレートは、プロジェクト項目またはプロジェクトを作成するために Visual Studio によって使用されるファイルを含む .zip ファイルです *。* 項目テンプレートとプロジェクトテンプレートの基礎の詳細については、「[プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)」を参照してください。

## <a name="create-item-templates"></a>項目テンプレートを作成する
 SharePoint プロジェクト項目の項目テンプレートを作成する場合、常に必要なファイルと、特定の種類のプロジェクト項目で使用される可能性があるオプションのファイルがあります。 SharePoint プロジェクト項目の種類を定義し、その項目テンプレートを作成する方法を示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」を参照してください。

 次の表に、SharePoint プロジェクトアイテムの項目テンプレートを作成するために必要なファイルを示します。

|必要なファイル|説明|
|-------------------|-----------------|
|*Sharepointprojectitem.spdata*ファイル|この XML ファイルは、プロジェクト項目の内容と既定の動作を指定します。 このファイルは、項目テンプレートに含まれている必要があります。 *Sharepointprojectitem.spdata*ファイルの内容の詳細については、「 [SharePoint プロジェクト項目スキーマリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)」を参照してください。|
|*.Vstemplate*ファイル。|このファイルには、 **[新しい項目の追加]** ダイアログボックスにテンプレートを表示し、テンプレートからプロジェクト項目を作成するために必要な情報が Visual Studio に用意されています。 このファイルは、項目テンプレートに含まれている必要があります。 詳細については、「 [Visual Studio テンプレートメタデータファイル](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装する Visual Studio 拡張機能アセンブリ。|このアセンブリは、プロジェクト項目の実行時の動作を定義します。 このアセンブリは、項目テンプレートを使用して VSIX パッケージに含める必要があります。 詳細については、「Visual Studio での sharepoint ツールの[カスタム sharepoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)」および「[拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。|

 次の表に、項目テンプレートに含めることができる最も一般的なオプションファイルを示します。 一部の種類のプロジェクト項目には、ここに記載されていない他のファイルが必要な場合があります。

| オプションファイル | 説明 |
|----------------------| - |
| *Elements .xml* | *フィーチャー要素*ファイル。 このファイルは、プロジェクト項目によって作成されたカスタマイズの UI と動作を定義します。 リストインスタンス、コンテンツの種類、カスタムアクションなど、それぞれの種類のカスタマイズには、このファイルの内容を定義する別のスキーマがあります。 詳細については、「[構成要素: 機能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))と[機能スキーマ](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))」を参照してください。 |
| *スキーマ .xml* | リスト定義のスキーマファイルです。 詳細については、「[構成要素: リストとドキュメントライブラリ](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))、および[.xml](/previous-versions/office/developer/sharepoint-2010/ms459356(v=office.14))」を参照してください。 |
| *webpart* | *Web パーツ定義*ファイル。 このファイルには、Web パーツのプロパティ設定が含まれています。 詳細については、「[ビルディングブロック: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。 |
| *.ascx* | ASP.NET UserControl ファイル。 このファイルは、視覚的 Web パーツの UI を定義します。 |
| *.aspx* | ASP.NET ページファイル。 このファイルには、アプリケーションページを定義する XML マークアップが含まれています。 |
| *.cs*または *.vb*ファイル | これらのコードファイルは、ビジュアルC#または Visual Basic コード (アプリケーションページ、Web パーツ、ワークフローなど) からアクセスできるプログラミングモデルを持つ SharePoint カスタマイズの動作を定義します。 |

## <a name="create-project-templates"></a>プロジェクト テンプレートを作成する
 SharePoint プロジェクトテンプレートを作成するときには、常に必要なファイルと、特定の種類のプロジェクトで使用される可能性があるオプションのファイルがあります。 通常、SharePoint プロジェクトには、SharePoint プロジェクトアイテムが少なくとも1つ含まれています。 ただし、これは必須ではありません。 たとえば、他のプロジェクトで作成された SharePoint ソリューションを配置するためにのみ使用することを目的とした SharePoint プロジェクトテンプレートを定義できます。

 SharePoint プロジェクト項目の種類を定義してそのプロジェクトテンプレートを作成する方法を示すチュートリアルについては、「[チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」を参照してください。

 次の表に、SharePoint プロジェクトテンプレートに含める必要があるファイルを示します。

|必要なファイル|説明|
|-------------------|-----------------|
|*.Vstemplate*ファイル|このファイルには、 **[新しいプロジェクト]** ダイアログボックスにテンプレートを表示し、テンプレートからプロジェクトを作成するために必要な情報が Visual Studio に用意されています。 詳細については、「 [Visual Studio テンプレートメタデータファイル](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))」を参照してください。|
|*.Csproj*ファイルまたは *.vbproj*ファイル|これはプロジェクトファイルです。 これにより、プロジェクトの内容と構成設定が定義されます。|
|*パッケージ*|このファイルは、プロジェクトの配置パッケージを定義します。 パッケージデザイナーを使用してプロジェクトのソリューションパッケージをカスタマイズすると、Visual Studio はソリューションパッケージに関するデータをこのファイルに格納します。<br /><br /> カスタム SharePoint プロジェクトテンプレートを作成するときは、最低限必要なコンテンツのみをパッケージファイルに含めることをお勧めします。また、拡張機能の <xref:Microsoft.VisualStudio.SharePoint.Packages> 名前空間の Api を使用してソリューションパッケージを構成することをお勧めし*ます。* は、プロジェクトテンプレートに関連付けられています。 この場合、プロジェクトテンプレートは、後で*パッケージパッケージ*ファイルの構造に変更が加えられたときに保護されます。 最低限必要なコンテンツのみを含む*パッケージ*ファイルを作成する例については、「[チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md))」を参照してください。<br /><br /> *パッケージのパッケージ*ファイルを直接変更する場合は、 *% Program Files (x86)% \ Microsoft Visual Studio 11.0 \ xml、xsd*のスキーマを使用して内容を確認できます。 (& c)|
|*パッケージ .xml*|このファイルは、プロジェクトから生成される SharePoint ソリューションパッケージ ( *.wsp*) のソリューションマニフェストファイル (*manifest.xml*) の基礎となります。 プロジェクトの種類のユーザーによる変更を意図していない動作を指定する場合は、このファイルにコンテンツを追加できます。 詳細については、「[構成要素: ソリューション](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))と[ソリューションスキーマ](/sharepoint/dev/schema/solution-schema)」を参照してください。<br /><br /> プロジェクトからソリューションパッケージをビルドすると、Visual Studio によって*パッケージ*の内容と*パッケージの .xml*ファイルがソリューションマニフェストファイルにマージされます。 ソリューションパッケージのビルドの詳細については、「[方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)する」を参照してください。|

 次の表に、プロジェクトテンプレートに含めることができるオプションのファイルを示します。

|オプションファイル|説明|
|-------------------|-----------------|
|SharePoint プロジェクト項目|SharePoint プロジェクト項目の種類を定義する1つ以上の sharepointprojectitem.spdata ファイルを含めることができます。 各*sharepointprojectitem.spdata*ファイルには、プロジェクトテンプレートを使用して VSIX パッケージに含まれる拡張機能アセンブリに一致する <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 実装が必要です。 詳細については、「[項目テンプレートを作成する](#create-item-templates)」を参照してください。<br /><br /> 通常、SharePoint プロジェクトには、SharePoint プロジェクトアイテムが少なくとも1つ含まれています。 ただし、これは必須ではありません。|
|*\<featureName >。*|このファイルは、配置のために複数のプロジェクト項目をグループ化するために使用される SharePoint 機能を定義します。 フィーチャーデザイナーを使用してプロジェクトの機能をカスタマイズすると、Visual Studio では、その機能に関するデータがこのファイルに格納されます。 プロジェクト項目を別の機能にグループ化する場合は、複数*の機能*ファイルを含めることができます。<br /><br /> カスタム SharePoint プロジェクトテンプレートを作成する場合は、各機能ファイルに最低限必要なコンテンツのみを含め、に関連付けられている拡張機能の <xref:Microsoft.VisualStudio.SharePoint.Features> 名前空間の Api を使用して機能を構成することをお勧めし*ます。* プロジェクトテンプレート。 これを行うと、プロジェクトテンプレートは、今後の*機能*ファイルの構造に変更されないように保護されます。 最低限必要なコンテンツのみを含む*機能*ファイルを作成する方法を示す例については、「[チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md))」を参照してください。<br /><br /> *機能*ファイルを直接変更する場合は、 *% Program Files (x86)% \ Microsoft Visual Studio 11.0 \ Xml\Schemas\FeatureModelSchema.xsd*のスキーマを使用して内容を確認できます。|
|*featureName > を\<します。テンプレート .xml*|このファイルは、プロジェクトから生成された各機能のフィーチャーマニフェストファイル (*system.xml*) の基礎となります。 プロジェクトの種類のユーザーによる変更を意図していない動作を指定する場合は、このファイルにコンテンツを追加できます。 詳細については、「[構成要素: 機能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))」および「[機能 .xml](/sharepoint/dev/schema/feature-xml-files)ファイル」を参照してください。<br /><br /> プロジェクトからソリューションパッケージをビルドすると、Visual Studio によって *\<featureName >* の各ペアの内容と\<featureName > がマージされ*ます。テンプレートの .xml*ファイルをフィーチャーマニフェストファイルにインポートします。 ソリューションパッケージのビルドの詳細については、「[方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)する」を参照してください。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>項目テンプレートとプロジェクトテンプレートのウィザードを作成する
 SharePoint プロジェクト項目の種類を定義し、項目またはプロジェクトテンプレートに関連付けると、ウィザードを作成することもできます。 開発者が項目テンプレートを使用して SharePoint プロジェクト項目をプロジェクトに追加するとき、または開発者がプロジェクトテンプレートを使用して SharePoint プロジェクト項目を含む新しいプロジェクトを作成するときに、ウィザードが表示されます。 ウィザードを使用して、開発者から情報を収集したり、新しい SharePoint プロジェクト項目を初期化したりすることができます。

 項目テンプレートとプロジェクトテンプレートのウィザードを作成する方法を示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成」、「パート 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md) 」、「[チュートリアル: プロジェクトを使用したサイト列プロジェクト項目の作成」を参照してください。テンプレート、パート 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>関連項目

- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
