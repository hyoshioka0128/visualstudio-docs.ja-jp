---
title: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成する
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
ms.openlocfilehash: c59a38e1153a57c1bd886121eeac244075045a42
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86017009"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成する
  開発用コンピューターでコマンドライン MSBuild タスクを使用して、SharePoint パッケージ (*.wsp*) のビルド、クリーン、検証を行うことができます。 これらのコマンドを使用して、ビルドコンピューターで Team Foundation Server を使用してビルドプロセスを自動化することもできます。

## <a name="build-a-sharepoint-package"></a>SharePoint パッケージの作成

#### <a name="to-build-a-sharepoint-package"></a>SharePoint パッケージをビルドするには

1. Windows の [**スタート**] メニューで、[**すべてのプログラム**] [  >  **アクセサリ**  >  **] [コマンドプロンプト**] の順に選択します。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージを作成します。 *Projectfilename*をプロジェクトの名前に置き換えます。

    ```cmd
    msbuild /t:Package ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトをパッケージ化することができます。

    ```cmd
    msbuild /t:Package ListDefinition1.vbproj
    msbuild /t:Package ListDefinition1.csproj
    ```

## <a name="clean-a-sharepoint-package"></a>SharePoint パッケージのクリーンアップ

#### <a name="to-clean-a-sharepoint-package"></a>SharePoint パッケージをクリーンアップするには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージをクリーンアップします。 *Projectfilename*をプロジェクトの名前に置き換えます。

    ```cmd
    msbuild /t:CleanPackage ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトをクリーンアップすることができます。

    ```cmd
    msbuild /t:CleanPackage ListDefinition1.vbproj
    msbuild /t:CleanPackage ListDefinition1.csproj
    ```

## <a name="validate-a-sharepoint-package"></a>SharePoint パッケージの検証

#### <a name="to-validate-a-sharepoint-package"></a>SharePoint パッケージを検証するには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージを検証します。 *Projectfilename*をプロジェクトの名前に置き換えます。

    ```cmd
    msbuild /t:ValidatePackage ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトを検証することができます。

    ```cmd
    msbuild /t:ValidatePackage ListDefinition1.vbproj
    msbuild /t:ValidatePackage ListDefinition1.csproj
    ```

## <a name="set-properties-in-a-sharepoint-package"></a>SharePoint パッケージのプロパティの設定

#### <a name="to-set-a-property-in-a-sharepoint-package"></a>SharePoint パッケージのプロパティを設定するには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージのプロパティを設定します。 *PropertyName*は、設定するプロパティで置き換えます。

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     たとえば、次のコマンドを実行して警告レベルを設定できます。

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>関連項目
- [SharePoint 機能の作成](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint 機能をカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能に項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
