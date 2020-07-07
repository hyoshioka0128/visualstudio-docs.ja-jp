---
title: SharePoint ソリューションのパッケージ化と配置 |Microsoft Docs
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9a4bf3394cf47b4f355fbe6a330ff5374e2da1c9
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015594"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>SharePoint ソリューションのパッケージ化と配置
  通常、SharePoint ソリューションは、ソリューションパッケージ (.wsp) ファイルを使用して SharePoint サーバーに配置されます。 Visual Studio を使用して、SharePoint プロジェクトアイテムをフィーチャーに整理し、SharePoint 機能を配置するためのパッケージを作成することができます。

 このトピックでは次の情報について説明します。

- [機能とパッケージの作成](#create-features-and-packages)

- [機能およびパッケージ化ツールのサポート](#feature-and-packaging-tool-support)

- [SharePoint ソリューションの配置](#deploy-sharepoint-solutions)

- [SharePoint ソリューションでのファイルの配置](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>機能とパッケージの作成
 Visual Studio を使用して、関連する SharePoint 要素を*機能*にグループ化することができます。 たとえば、連絡先リスト定義の機能には、リストインスタンスとリスト定義を含めることができます。 これらの2つの要素を組み合わせて、デプロイの目的で1つの機能にすることができます。 機能の詳細については、「[ビルディングブロック: features](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))」を参照してください。

 次に、複数の機能、サイト定義、アセンブリ、およびその他のファイルを1つのパッケージにバンドルする SharePoint ソリューションパッケージ (*.wsp*) を作成できます。これにより、ファイルを sharepoint がサーバーに配置するために必要な形式でファイルが格納されます。 詳細については、「[ビルディングブロック: Solutions](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))」を参照してください。

## <a name="feature-and-packaging-tool-support"></a>機能およびパッケージ化ツールのサポート
 Visual Studio の SharePoint 開発ツールを使用すると、簡単に配置できるように SharePoint ファイルを機能やソリューションパッケージにすばやく整理できます。 機能とソリューションパッケージを構成するには、次のツールを使用できます。

- フィーチャーデザイナーとパッケージデザイナー。

- ツールウィンドウであるパッケージングエクスプローラー。

- ソリューション エクスプローラー。

### <a name="feature-designer-and-package-designer"></a>フィーチャーデザイナーとパッケージデザイナー
 フィーチャーデザイナーを使用して、機能を作成し、スコープを設定し、他の機能を依存関係としてマークできます。 また、デザイナーには、各機能について記述した最終的な XML ファイルも表示されます。 詳細については、「 [SharePoint 機能の作成](../sharepoint/creating-sharepoint-features.md)」を参照してください。

 フィーチャーデザイナーで*スコープ*を設定して、特定の web サイトまたは web サイトのグループに機能を適用します。 1つの機能が個々の Web サイトに対してアクティブ化されている場合、機能はその特定の Web サイトでのみ機能します。 サイトコレクションに対して機能がアクティブになっている場合、その機能の項目はサイトコレクション全体に適用されます。 詳細については、「 [Element Scope](/previous-versions/office/developer/sharepoint-2010/ms476615(v=office.14))」を参照してください。

 機能が他の機能に依存している場合は、機能を使用できるようにする前に、機能の*アクティブ化の依存関係*を設定して、依存する機能をマークすることができます。 フィーチャーのアクティブ化依存関係は、依存する機能がそのスコープで既にアクティブ化されているかどうかを確認します。 詳細については、「[アクティブ化の依存関係とスコープ](/previous-versions/office/developer/sharepoint-2010/aa543162(v=office.14))」を参照してください。

 パッケージデザイナーでは、SharePoint 要素を1つのソリューションパッケージにグループ化し、配置時に Web サーバーをリセットするかどうかを構成できます。 配置サーバーの種類を設定するには、[**プロパティ**] ウィンドウを使用します。 また、デザイナーは、パッケージの内容を記述する XML ファイルも生成します。 詳細については、「 [SharePoint ソリューションパッケージの作成](../sharepoint/creating-sharepoint-solution-packages.md)」を参照してください。

 デプロイ中に、インターネットインフォメーションサービス (IIS) サービスが停止して、ソリューションファイルが SharePoint サーバーにコピーされます。 Visual Studio のパッケージデザイナーを使用して、Web サーバーを再起動するかどうかを選択できます。 ソリューションをフロントエンド Web サーバーまたはアプリケーションサーバーに配置するかどうかを構成するには、[**プロパティ**] ウィンドウを使用します。 詳細については、「 [Solution Element (solution)](/previous-versions/office/developer/sharepoint-2010/ms412929(v=office.14))」を参照してください。

### <a name="packaging-explorer"></a>パッケージングエクスプローラー
 フィーチャーデザイナーとパッケージデザイナーを補完するには、パッケージングエクスプローラーを使用して、SharePoint ファイルを機能やパッケージにグループ化します。 さらに、パッケージ、機能、SharePoint プロジェクトアイテム、およびファイルの階層ビューを表示できます。 パッケージングエクスプローラーは、次のタスクを完了するために使用できるツールウィンドウです。

- SharePoint プロジェクトのアイテムとファイルを開きます。

- SharePoint プロジェクトアイテムをフィーチャー間でドラッグアンドドロップします。

- SharePoint プロジェクトのアイテムとフィーチャーをパッケージ間でドラッグアンドドロップします。

- パッケージに新しい機能を追加します。

- 機能またはパッケージデザイナーを開きます。

- 機能とパッケージを検証します。

  Visual Studio の SharePoint 開発ツールには、ソリューションパッケージの形式が正しいことを確認するための検証規則が用意されています。 また、このルールによって、 *.wsp*ソリューションファイルが SharePoint サーバーで正常に配置およびアクティブ化できることが確認されます。 機能の XML スキーマの詳細については、「[機能スキーマ](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))」を参照してください。

  SharePoint プロジェクトシステムには、カスタム機能およびパッケージ検証規則を追加できます。 詳細については、「[方法: SharePoint ソリューションのカスタム機能およびパッケージ検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。

  パッケージングエクスプローラーの詳細については、「[方法: パッケージングエクスプローラーを使用してパッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

### <a name="solution-explorer"></a>ソリューション エクスプローラー
 ソリューションエクスプローラーを使用すると、SharePoint プロジェクトのファイルを移動して開くことができます。 ソリューションエクスプローラーのコンテキストメニューを使用して、機能、機能イベントレシーバー、および機能リソースを追加します。 さらに、フィーチャーデザイナーとパッケージデザイナーを開いて、デプロイ用の機能とパッケージを構成することもできます。

## <a name="deploy-sharepoint-solutions"></a>SharePoint ソリューションの配置
 Visual Studio で機能とパッケージをカスタマイズした後、SharePoint サーバーに配置する *.wsp*ファイルを作成できます。 Visual Studio を使用して、のデバッグとテストを行うことができます。開発用コンピューター上の SharePoint サーバー上の*wsp*のみ。 SharePoint ソリューションをリモート SharePoint サーバーに配置する方法の詳細については、「[ソリューションの配置](/previous-versions/office/developer/sharepoint-2010/aa544500(v=office.14))」を参照してください。

 開発用コンピューターの配置手順をカスタマイズすることもできます。 詳細については、「 [SharePoint ソリューションパッケージの配置、発行、およびアップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)」を参照してください。

## <a name="deploy-files-in-sharepoint-solutions"></a>SharePoint ソリューションでのファイルの配置
 通常、sharepoint プロジェクトアイテムを SharePoint ソリューションに追加すると、必要なすべてのファイルが含まれます。 コンパイルできるファイル (コードファイル) は、ソリューションの出力アセンブリに組み込まれています。 ただし、 *.xml*、 *.txt*、リソースファイルなど、コンパイルできないファイルを SharePoint プロジェクトに追加することが必要になる場合もあります。 これらのファイルは、ソリューションに自動的にパッケージ化されません。 パッケージが確実にパッケージ化されるようにするには、マップされたフォルダーまたは SharePoint プロジェクトアイテムにファイルを追加します。

 マップされたフォルダーに追加されたファイルは、ソリューションの配置時に SharePoint hive に自動的にコピーされます。 SharePoint プロジェクト項目に追加されたファイルは、各ファイルの [**配置場所**] プロパティで指定された場所に配置されます。これは、"**展開の種類**" プロパティに基づいて部分的に設定されます。 既定では、[**展開の種類**] プロパティの値は**nodeployment**です。これは、ファイルがソリューションと共に配置されないことを意味します。 パッケージにファイルを含めるには、プロパティに別の値を設定する必要があります。

 たとえば、 *.xml*ファイルを SharePoint プロジェクトに追加するには、次のいずれかの操作を実行します。

- SharePoint "レイアウト" のマップされたフォルダーをプロジェクトに追加します。 これにより、プロジェクトのサブフォルダーを持つ**レイアウト**という名前のフォルダー**ソリューションエクスプローラー**に作成されます。 *.Xml*ファイルを新しいサブフォルダーに追加します。 既定では、ファイルは、の下の SharePoint ファイルシステムに配置されます *。\ テンプレート \ レイアウト \\ \<Folder Name> *。 マップされたフォルダーを追加する方法については、「[方法: マップされたフォルダーを追加および削除](../sharepoint/how-to-add-and-remove-mapped-folders.md)する」を参照してください。

- *.Xml*ファイルを SharePoint プロジェクトアイテムのフォルダーに追加し、 *.xml*ファイルの [配置の**種類**] プロパティを [ **nodeployment** ] から [ **rootfile** ] や [ **elementfile**] などの別の設定に変更します。 適切な**展開の種類**の設定は、ファイルとプロジェクトによって異なります。 **展開の種類**のプロパティ設定の詳細については、「 [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」を参照してください。

  追加したファイルがソリューション内の特定のプロジェクトに適用されない場合は、ソリューションに空の SharePoint プロジェクトを追加して、追加のファイルを追加することができます。 また、SharePoint にファイルを配置する別の方法として、特にコンテンツデータベースにモジュールを追加する方法もあります。そのためには、モジュールをプロジェクトに追加し、ファイルをモジュールに追加します。 詳細については、「[モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
