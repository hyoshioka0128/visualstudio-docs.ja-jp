---
title: '方法 : ビルド出力ディレクトリを変更する'
ms.date: 05/15/2019
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- output directory, changing
ms.assetid: a8333c89-afb2-4b1d-b2e2-9146da852402
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e4c2f2445bc7139c5bbc80a35905e24c319c9dfa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85284647"
---
# <a name="how-to-change-the-build-output-directory"></a>方法 : ビルド出力ディレクトリを変更する

(デバッグ、リリース、またはその両方の) 構成ごとにプロジェクトによって生成された出力の場所を指定できます。

## <a name="change-the-build-output-directory"></a>ビルド出力ディレクトリを変更する

1. プロジェクトのプロパティ ページを開くには、**ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[プロパティ]** を選択します。

2. プロジェクトの種類に基づいてタブを選択します。

   - C# の場合、 **[ビルド]** タブを選択します。
   - Visual Basic の場合、 **[コンパイル]** タブを選択します。
   - C++ または JavaScript の場合、 **[全般]** タブを選択します。

3. 上部にある構成のドロップダウンで、出力ファイルの場所を変更する構成を選択します (**デバッグ**、**リリース**、または**すべての構成**)。

4. ページで出力パス エントリを見つけます。これはプロジェクトの種類によって異なります。

   - C# プロジェクトと JavaScript プロジェクトの**出力パス**
   - Visual Basic プロジェクトの**ビルド出力パス**
   - Visual C++ プロジェクトの**出力ディレクトリ**

   出力の生成先とするパスを入力するか (ルート プロジェクト ディレクトリの絶対パスまたは相対パス)、 **[参照]** を選択し、そのフォルダーを代わりに参照します。

   ![Visual Studio C# プロジェクトの出力パス プロパティ](media/output-path.png)
   
   > [!NOTE]
   > 既定では、一部のプロジェクトで、フレームワークとランタイムがビルド パスに含まれます。 これを変更するには、**ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[プロジェクト ファイルの編集]** を選択して、以下を追加します。
   > ```xml
   > <PropertyGroup>
   >   <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
   >   <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
   > </PropertyGroup>
   > ```

> [!TIP]
> 指定した場所に出力が生成されない場合、Visual Studio のメニュー バーで選択し、該当する構成 (**デバッグ**や**リリース**など) を構築していることを確認してください。
>
> ![Visual Studio 2019 のビルド構成ピッカー](media/build-configuration-chooser.png)

## <a name="see-also"></a>参照

- [[ビルド] ページ (プロジェクト デザイナー) (C#)](../ide/reference/build-page-project-designer-csharp.md)
- [[全般] プロパティ ページ (プロジェクト)](/cpp/build/reference/general-property-page-project)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
