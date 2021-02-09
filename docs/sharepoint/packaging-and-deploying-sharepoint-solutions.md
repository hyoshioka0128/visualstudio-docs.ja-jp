---
title: SharePoint ソリューションのパッケージ化と配置 | Microsoft Docs
description: SharePoint ソリューションをパッケージ化して配置します。これはソリューション パッケージ (.wsp) ファイルを使用して SharePoint サーバーに配置されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- packaging [SharePoint development in Visual Studio]
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, packaging and deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ae74aa3cf759ba006acd36c168eecceac4b2ee4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916545"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>SharePoint ソリューションのパッケージ化と配置
  通常、SharePoint ソリューションは、ソリューション パッケージ (.wsp) ファイルを使用して SharePoint サーバーに配置されます。 Visual Studio を使用して、SharePoint プロジェクト項目をフィーチャーに整理したり、パッケージを作成して SharePoint フィーチャーを配置したりできます。

 このトピックでは次の情報について説明します。

- [フィーチャーとパッケージを作成する](#create-features-and-packages)

- [フィーチャーとパッケージング ツールのサポート](#feature-and-packaging-tool-support)

- [SharePoint ソリューションを配置する](#deploy-sharepoint-solutions)

- [SharePoint ソリューションにファイルを配置する](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>フィーチャーとパッケージを作成する
 Visual Studio を使用して、関連する SharePoint 要素を "*フィーチャー*" にグループ化できます。 たとえば、連絡先リスト定義のフィーチャーに、リスト インスタンスとリスト定義を含めることができます。 これらの 2 つの要素を組み合わせて、配置の目的で 1 つのフィーチャーにすることができます。 フィーチャーの詳細については、「[文書パーツ: フィーチャー](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))」を参照してください。

 次に、SharePoint ソリューション パッケージ ( *.wsp*) を作成して、複数のフィーチャー、サイト定義、アセンブリ、およびその他のファイルを 1 つのパッケージにバンドルすることができます。これには、SharePoint でファイルをサーバーに配置するために必要な形式でファイルが保存されます。 詳細については、「[文書パーツ: 「解決方法」](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))を参照してください。

## <a name="feature-and-packaging-tool-support"></a>フィーチャーとパッケージング ツールのサポート
 Visual Studio の SharePoint 開発ツールを使用すると、配置を簡単に行うために SharePoint ファイルをフィーチャーやソリューション パッケージにすばやく整理できます。 フィーチャーとソリューション パッケージを構成するには、次のツールを使用します。

- フィーチャー デザイナーとパッケージ デザイナー。

- ツール ウィンドウであるパッケージング エクスプローラー。

- ソリューション エクスプローラー。

### <a name="feature-designer-and-package-designer"></a>フィーチャー デザイナーとパッケージ デザイナー
 フィーチャー デザイナーを使用して、フィーチャーを作成したり、スコープを設定したり、他のフィーチャーを依存関係としてマークしたりできます。 また、このデザイナーには、各フィーチャーについて記述する最終的な XML ファイルも表示されます。 詳細については、「[SharePoint フィーチャーの作成](../sharepoint/creating-sharepoint-features.md)」を参照してください。

 フィーチャー デザイナーで "*スコープ*" を設定して、特定の Web サイト、または Web サイトのグループにフィーチャーを適用します。 フィーチャーが個々の Web サイトに対してアクティブ化されている場合、フィーチャーはその特定の Web サイトでのみ機能します。 フィーチャーがサイト コレクションに対してアクティブ化されている場合、フィーチャーの項目はサイト コレクション全体に適用されます。 詳細については、「[要素のスコープ](/previous-versions/office/developer/sharepoint-2010/ms476615(v=office.14))」を参照してください。

 フィーチャーが他のフィーチャーに依存している場合は、フィーチャーを使用できるようにする前に、*フィーチャー アクティブ化依存関係* を設定して、依存しているフィーチャーをマークすることができます。 フィーチャー アクティブ化依存関係では、依存しているフィーチャーがそのスコープで既にアクティブ化されているかどうかが確認されます。 詳細については、「[アクティブ化依存関係とスコープ](/previous-versions/office/developer/sharepoint-2010/aa543162(v=office.14))」を参照してください。

 パッケージ デザイナーでは、SharePoint 要素を 1 つのソリューション パッケージにグループ化し、配置時に Web サーバーをリセットするかどうかを構成することができます。 配置サーバーの種類を設定するには、 **[プロパティ]** ウィンドウを使用します。 また、このデザイナーでは、パッケージの内容を記述する XML ファイルも生成されます。 詳細については、「[SharePoint ソリューション パッケージの作成](../sharepoint/creating-sharepoint-solution-packages.md)」を参照してください。

 配置時に、インターネット インフォメーション サービス (IIS) サービスが停止されて、ソリューション ファイルが SharePoint サーバーにコピーされます。 Visual Studio のパッケージ デザイナーを使用して、Web サーバーを再起動するかどうかを選択できます。 ソリューションをフロントエンド Web サーバーとアプリケーション サーバーのどちらに配置するかを構成するには、 **[プロパティ]** ウィンドウを使用します。 詳細については、「[Solution 要素 (ソリューション)](/previous-versions/office/developer/sharepoint-2010/ms412929(v=office.14))」を参照してください。

### <a name="packaging-explorer"></a>パッケージング エクスプローラー
 フィーチャー デザイナーとパッケージ デザイナーを補完するには、パッケージング エクスプローラーを使用して、SharePoint ファイルをフィーチャーやパッケージにグループ化します。 さらに、パッケージ、フィーチャー、SharePoint プロジェクト項目、およびファイルの階層ビューを表示できます。 パッケージング エクスプローラーは、次のタスクを実行するために使用できるツール ウィンドウです。

- SharePoint プロジェクト項目とファイルを開く。

- SharePoint プロジェクト項目をフィーチャー間でドラッグ アンド ドロップする。

- SharePoint プロジェクト項目とフィーチャーをパッケージ間でドラッグ アンド ドロップする。

- 新しいフィーチャーをパッケージに追加する。

- フィーチャーまたはパッケージ デザイナーを開く。

- フィーチャーとパッケージを検証する。

  Visual Studio の SharePoint 開発ツールには、ソリューション パッケージの形式が正しいことを確認するための検証規則が用意されています。 また、この規則では、SharePoint サーバーで *.wsp* ソリューション ファイルを正常に配置およびアクティブ化できることが検証されます。 フィーチャーの XML スキーマの詳細については、「[フィーチャー スキーマ](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))」を参照してください。

  SharePoint プロジェクト システムには、フィーチャーとパッケージのカスタム検証規則を追加できます。 詳細については、「[方法:SharePoint ソリューションのフィーチャーとパッケージのカスタム検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。

  パッケージング エクスプローラーの詳細については、「[方法: パッケージング エクスプローラーを使用してパッケージのフィーチャーおよび項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

### <a name="solution-explorer"></a>ソリューション エクスプローラー
 ソリューション エクスプローラーを使用すると、SharePoint プロジェクトのファイルに移動して開くことができます。 ソリューション エクスプローラーのコンテキスト メニューを使用して、フィーチャー、フィーチャー イベント レシーバー、およびフィーチャー リソースを追加します。 さらに、フィーチャー デザイナーとパッケージ デザイナーを開いて、配置のためにフィーチャーとパッケージを構成することもできます。

## <a name="deploy-sharepoint-solutions"></a>SharePoint ソリューションを配置する
 Visual Studio でフィーチャーとパッケージをカスタマイズした後、 *.wsp* ファイルを作成して SharePoint サーバーに配置することができます。 Visual Studio を使用して、開発用コンピューター上の SharePoint サーバーでのみ、*wsp* のデバッグとテストを行うことができます。 SharePoint ソリューションをリモート SharePoint サーバーに配置する方法の詳細については、[ソリューションの配置](/previous-versions/office/developer/sharepoint-2010/aa544500(v=office.14))に関するページを参照してください。

 また、開発用コンピューターでの配置手順をカスタマイズすることもできます。 詳細については、「[SharePoint ソリューション パッケージの配置、発行、アップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)」を参照してください。

## <a name="deploy-files-in-sharepoint-solutions"></a>SharePoint ソリューションにファイルを配置する
 通常、SharePoint プロジェクト項目を SharePoint ソリューションに追加すると、必要なすべてのファイルが含まれます。 コンパイルできるファイル (コード ファイル) は、ソリューションの出力アセンブリに組み込まれています。 ただし、コンパイルできないファイル ( *.xml*、 *.txt*、リソース ファイルなど) を SharePoint プロジェクトに追加することが必要になる場合もあります。 これらのファイルは、ソリューションに自動的にパッケージ化されません。 パッケージが確実にパッケージ化されるようにするには、マップされたフォルダーまたは SharePoint プロジェクト項目にファイルを追加します。

 マップされたフォルダーに追加されたファイルは、ソリューションの配置時に SharePoint hive に自動的にコピーされます。 SharePoint プロジェクト項目に追加されたファイルは、各ファイルの **[配置場所]** プロパティで指定された場所に配置されます。これは、部分的に **[配置の種類]** プロパティに基づいて設定されます。 既定では、 **[配置の種類]** プロパティ値は **NoDeployment** (ファイルがソリューションと共に配置されない) になります。 パッケージにファイルを含めるには、プロパティに別の値を設定する必要があります。

 たとえば、 *.xml* ファイルを SharePoint プロジェクトに追加するには、次のいずれかの操作を実行します。

- SharePoint "Layouts" のマップされたフォルダーをプロジェクトに追加します。 これにより、**ソリューション エクスプローラー** に、プロジェクトのサブフォルダーを含む **Layouts** という名前のフォルダーが作成されます。 *.xml* ファイルを新しいサブフォルダーに追加します。 既定では、このファイルは *..\TEMPLATE\LAYOUTS\\\<Folder Name>* の下にある SharePoint ファイル システムに配置されます。 マップされたフォルダーを追加する方法の詳細については、「[方法: マップされたフォルダーを追加および削除する](../sharepoint/how-to-add-and-remove-mapped-folders.md)」を参照してください。

- *.xml* ファイルを SharePoint プロジェクト項目のフォルダーに追加します。次に、 *.xml* ファイルの **[配置の種類]** プロパティを **NoDeployment** から別の設定 (**RootFile** や **ElementFile** など) に変更します。 **[配置の種類]** の適切な設定は、ファイルとプロジェクトによって異なります。 **[配置の種類]** プロパティ設定の詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」を参照してください。

  追加したファイルがソリューション内の特定のプロジェクトに適用されない場合は、空の SharePoint プロジェクトをソリューションに追加してから、追加のファイルを追加することができます。 また、ファイルを SharePoint (特にコンテンツ データベース) に配置する別の方法として、モジュールをプロジェクトに追加してから、ファイルをモジュールに追加します。 詳細については、「[モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
