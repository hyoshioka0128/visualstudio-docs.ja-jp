---
title: 1つのソリューションで複数の Dsl をMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 7e668620-6217-4e87-aea7-e9036776c8e4
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9a3b35e05108db879b365b9cafc39cacdf843397
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668551"
---
# <a name="multiple-dsls-in-one-solution"></a>1 つのソリューション内の複数の DSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

いくつかの DSL を単一ソリューションの一部としてパッケージ化し、同時にインストールすることができます。

 複数の DSL を統合するためにいくつかの手法を使用できます。 詳細については、「 [Visual Studio Modelbus を使用](../modeling/integrating-models-by-using-visual-studio-modelbus.md) したモデルの統合」および「 [方法: ドラッグアンドドロップハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md) 」および「 [コピー動作をカスタマイズ](../modeling/customizing-copy-behavior.md)する」を参照してください。

### <a name="to-build-more-than-one-dsl-in-the-same-solution"></a>複数の DSL を同じソリューションの中にビルドするには

1. 2 つ以上の DSL ソリューションと 1 つの VSIX プロジェクトを作成し、すべてのプロジェクトを単一のソリューションに追加します。

   - 新しい VSIX プロジェクトを作成するには、[ **新しいプロジェクト** ] ダイアログで、[ **Visual C#**]、[ **機能拡張**]、[ **VSIX プロジェクト**] の選択します。

   - VSIX ソリューション ディレクトリ内に 2 つ以上の DSL ソリューションを作成します。

        各 DSL について、Visual Studio の新しいインスタンスを開きます。 新しい DSL を作成し、同じソリューション フォルダとして VSIX ソリューションを指定します。

        各 DSL は異なるファイル拡張子名を付けて作成します。

   - **Dsl**および**dslpackage**プロジェクトの名前を変更して、それらがすべて異なっているようにします。 たとえば、`Dsl1`、`DslPackage1`、`Dsl2`、`DslPackage2` のようになります。

   - 各 **Dslpackage \* \ source.extension.tt**で、次の行を正しい Dsl プロジェクト名に更新します。

        `string dslProjectName = "Dsl2";`

   - VSIX ソリューションで、Dsl * および DslPackage プロジェクトを追加し \* ます。

        各ペアを独自のソリューション フォルダーに配置することを推奨します。

2. 以下のように DSL の VSIX マニフェストを結合します。

   1. _Yourvsixproject 配置_**\source.extension.manifest**を開きます。

   2. DSL ごとに、[ **コンテンツの追加** ] を選択し、次のように追加します。

       - `Dsl*`**MEF コンポーネント**としてのプロジェクト

       - `DslPackage*`**MEF コンポーネント**としてのプロジェクト

       - `DslPackage*`**VS パッケージ**としてのプロジェクト

3. ソリューションをビルドします。

   この結果の VSIX では両方の DSL がインストールされます。 F5 キーを使用してテストすることも、 _yourvsixproject 配置_を配置することも**できます。 \\ \* **

## <a name="see-also"></a>参照
 [Visual Studio Modelbus を使用したモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)[方法: ドラッグアンドドロップハンドラーを追加](../modeling/how-to-add-a-drag-and-drop-handler.md)して[コピー動作をカスタマイズ](../modeling/customizing-copy-behavior.md)する
