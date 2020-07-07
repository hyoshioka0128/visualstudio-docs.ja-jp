---
title: '方法: 追加のアセンブリを追加および削除するMicrosoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.CustomAssembly
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 07b9016a4e246d3ed5a2697d924f556517a8226f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014829"
---
# <a name="how-to-add-and-remove-additional-assemblies"></a>方法: 追加のアセンブリを追加および削除する
  SharePoint パッケージが機能またはデータについて他のアセンブリに依存している場合、そのアセンブリをソリューション パッケージ (.wsp) に追加できます。 パッケージをインストールする際は、カスタム アセンブリがインストールされているかどうかが、SharePoint サーバーによって確認されます。

 アセンブリに関連付けられているセーフ コントロールやクラス リソース ファイルを追加および変更することもできます。

## <a name="add-additional-assemblies-safe-controls-and-class-resources"></a>アセンブリ、セーフコントロール、およびクラスリソースを追加する
 SharePoint ソリューション パッケージにアセンブリを追加できます。 サンドボックス ソリューションの追加アセンブリは、グローバル アセンブリ キャッシュに配置されますが、サンドボックス ソリューションの SharePoint プロジェクト項目はコンテンツ データベースに追加されます。 これらの追加アセンブリにセーフ コントロールやクラス リソースを追加することもできます。 安全なコントロールの詳細については、「 [SharePoint Foundation での Web パーツの配置](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))」の「[プロジェクト項目でのパッケージ化と配置に関する情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」または「SafeControl エントリの作成」を参照してください。

#### <a name="to-add-an-existing-assembly"></a>既存のアセンブリを追加するには

1. **パッケージデザイナー**を開きます。 詳細については、「[方法: SharePoint ソリューションパッケージをカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)する」を参照してください。

2. **[詳細]** タブを選択します。

3. [**追加**] ボタンをクリックし、一覧から [**既存のアセンブリの追加**] を選択します。

     [**既存のアセンブリの追加**] ダイアログボックスが表示されます。

4. 省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択し、追加するアセンブリを選択します。 移植性を考慮して、選択したアセンブリへの相対パスを使用することをお勧めします。

5. **配置ターゲット**の場合は、[ **globalassemblycache** ] オプションボタンをクリックしてアセンブリをグローバルアセンブリキャッシュに配置するか、[ **webapplication** ] オプションボタンをクリックして、SharePoint を実行しているサーバー上の webapplication フォルダーにアセンブリを配置します。

#### <a name="to-add-an-assembly-from-project-output"></a>プロジェクトの出力からアセンブリを追加するには

1. **パッケージデザイナー**を開きます。

     詳細については、「[方法: SharePoint ソリューションパッケージをカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)する」を参照してください。

2. **[詳細]** タブを選択します。

3. [**追加**] ボタンをクリックし、一覧から [**プロジェクト出力からアセンブリを追加**] を選択します。

     [**プロジェクト出力からアセンブリを追加**] ダイアログボックスが表示されます。

4. [**ソースプロジェクト**] ボックスの一覧で、追加するソースプロジェクトを選択します。

5. **配置ターゲット**の場合は、[ **globalassemblycache** ] オプションボタンをクリックしてアセンブリをグローバルアセンブリキャッシュに配置するか、[ **webapplication** ] オプションボタンをクリックして、SharePoint を実行しているサーバー上の webapplication フォルダーにアセンブリを配置します。

#### <a name="to-add-a-safe-control"></a>セーフ コントロールを追加するには

1. [**既存のアセンブリの編集**] ダイアログボックスを開きます。 これを行うには、パッケージデザイナーを開き、[**詳細設定**] タブを選択し、アセンブリを選択して、[**編集**] ボタンをクリックします。

2. [**セーフコントロール**] ウィンドウで、 **[ここをクリックして新しい項目を追加**します] ボタンを選択します。

3. [**アセンブリ名**] 列に、アセンブリの名前を入力します。

4. [**名前空間**] 列に、セーフコントロールの名前空間の名前を入力します。

5. [**型名**] 列に、型の名前を入力します。

#### <a name="to-add-a-class-resource"></a>クラス リソースを追加するには

1. [**既存のアセンブリの編集**] ダイアログボックスを開きます。 これを行うには、パッケージデザイナーを開き、[**詳細設定**] タブを選択し、アセンブリを選択して、[**編集**] ボタンをクリックします。

2. [**クラスリソース**] ウィンドウで、 **[ここをクリックして新しい項目を追加**します] ボタンを選択します。

3. [**ファイル名**] 列で省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択し、追加するクラスリソースを選択します。

## <a name="delete-custom-assemblies"></a>カスタムアセンブリの削除
 SharePoint パッケージからアセンブリを削除したり、既存のアセンブリからセーフ コントロールやクラス リソースを削除することもできます。

#### <a name="to-delete-an-existing-assembly"></a>既存のアセンブリを削除するには

1. **パッケージデザイナー**を開きます。 詳細については、「[方法: SharePoint ソリューションパッケージをカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)する」を参照してください。

2. **[詳細]** タブを選択します。

3. [**追加のアセンブリ**] ペインで、削除するカスタムアセンブリを選択します。

4. **[削除]** をクリックします。

#### <a name="to-delete-a-safe-control-for-an-assembly"></a>アセンブリの安全なコントロールを削除するには

1. [**既存のアセンブリの編集**] ダイアログボックスを開きます。 これを行うには、パッケージデザイナーを開き、[**詳細設定**] タブを選択し、アセンブリを選択して、[**編集**] ボタンをクリックします。

2. 削除する安全なコントロールをクリックします。

3. Del キーを押します。

#### <a name="to-delete-a-class-resource-for-an-assembly"></a>アセンブリのクラス リソースを削除するには

1. [**既存のアセンブリの編集**] ダイアログボックスを開きます。 これを行うには、パッケージデザイナーを開き、[**詳細設定**] タブを選択し、アセンブリを選択して、[**編集**] ボタンをクリックします。

2. 削除するクラス リソースをクリックします。

3. Del キーを押します。

## <a name="see-also"></a>関連項目
- [SharePoint 機能の作成](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能に項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
