---
title: MSBuild ターゲットを使用して SharePoint ソリューションパッケージをカスタマイズする
titleSuffix: ''
description: コマンドプロンプトで MSBuild ターゲットを使用して、Visual Studio で SharePoint ソリューションパッケージファイル (.wsp) を作成する方法をカスタマイズします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 5aa0afbe685c85d9a005dc621f58f17d396c0236
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903651"
---
# <a name="how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets"></a>方法: MSBuild ターゲットを使用して SharePoint ソリューションパッケージをカスタマイズする
  MSBuild ターゲットをコマンドプロンプトで使用することにより、Visual Studio が SharePoint パッケージファイル (*.wsp*) を作成する方法をカスタマイズできます。 たとえば、MSBuild のプロパティをカスタマイズして、パッケージ化された中間ディレクトリと、列挙されたファイルを指定する MSBuild 項目グループを変更できます。

## <a name="customize-and-run-msbuild-targets"></a>MSBuild ターゲットのカスタマイズと実行
 BeforeLayout および AfterLayout ターゲットをカスタマイズする場合は、パッケージレイアウトの前に、パッケージ化されるファイルの追加、削除、変更などのタスクを実行できます。

#### <a name="to-customize-the-beforelayout-target"></a>BeforeLayout ターゲットをカスタマイズするには

1. メモ帳などのエディターを開き、次のコードを追加します。

   ```xml
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <Target Name="BeforeLayout">
       <Message Importance="high" Text="In the BeforeLayout Target"></Message>
     </Target>
   </Project>
   ```

    この例では、このターゲットのパッケージ化の前にメッセージを表示します。

2. ファイルに「 **Customlayout. sharepoint**」という名前を付け、sharepoint プロジェクトのフォルダーに保存します。

3. プロジェクトを開き、ショートカットメニューを開き、[ **プロジェクトのアンロード**] を選択します。

4. **ソリューションエクスプローラー** で、プロジェクトのショートカットメニューを開き、[ *\<ProjectName> .vbproj* の **編集**] または [ *\<ProjectName> .csproj* の **編集**] を選択します。

5. `Import`プロジェクトファイルの末尾付近にある行の後に、次の行を追加します。

   ```xml
   <Import Project="CustomLayout.SharePoint.targets" />
   ```

6. プロジェクト ファイルを保存して閉じます。

7. **ソリューションエクスプローラー** で、プロジェクトのショートカットメニューを開き、[プロジェクトの **再読み込み**] をクリックします。

   プロジェクトを発行すると、パッケージが開始される前に、メッセージが出力に表示されます。

#### <a name="to-customize-the-afterlayout-target"></a>AfterLayout ターゲットをカスタマイズするには

1. メニューバーで、[**ファイル**] [ファイルを開く] の順に選択し  >  **Open**  >  **File** ます。

2. [ **ファイルを開く** ] ダイアログボックスで、プロジェクトフォルダーに移動し、customlayout. target ファイルを選択して、[ **開く** ] をクリックします。

3. タグの直前に `</Project>` 、次のコードを追加します。

   ```xml
   <Target Name="AfterLayout">
     <Message Importance="high" Text="In the AfterLayout Target"></Message>
   </Target>
   ```

    この例では、このターゲットがパッケージ化された後にメッセージを表示します。

4. ターゲットファイルを保存して閉じます。

5. Visual Studio を再起動し、プロジェクトを開きます。

   プロジェクトを発行すると、パッケージの開始前に BeforeLayout メッセージが表示され、パッケージの終了後に AfterLayout メッセージが表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
