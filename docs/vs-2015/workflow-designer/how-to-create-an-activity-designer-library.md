---
title: '方法: アクティビティデザイナーライブラリを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5b62e092-63b3-462d-9d77-fb112482f45d
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 63404d3d81c44ac4b8308d949cdb87df419f2e04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662873"
---
# <a name="how-to-create-an-activity-designer-library"></a>アクティビティ デザイナー ライブラリを作成する方法
カスタム アクティビティ デザイナーを使用して、標準アクティビティやカスタム アクティビティのためのユーザー インターフェイスを作成できます。 ユーザー インターフェイスが複雑にならないようにして、1 つのアクティビティに対応するアクティビティ デザイナーを複数作成することができます。 このシナリオでは、複数の対象に対応したデザイナーを作成できます。

### <a name="to-create-an-activity-designer-library"></a>アクティビティ デザイナー ライブラリを作成するには

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)]を起動します。

2. [**ファイル**] メニューの [**新規作成**] をポイントし、[**プロジェクト**] を選択します。 を選択すると、[ **新しいプロジェクト** ] ダイアログボックスが開きます。

3. [**プロジェクトの種類**] ペインで、優先する言語に応じて、 **Visual C#** または**Visual Basic**グループから [**ワークフロー** ] を選択します。

4. [ **テンプレート** ] ペインで、[ **アクティビティデザイナーライブラリ**] を選択します。

5. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

6. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

7. [ **ソリューション** ] ボックスにソリューションの内容を示す名前を入力し、[ **OK]** をクリックします。

    > [!NOTE]
    > ワークフローコンソールアプリケーションを既存のソリューションに追加する場合は、でそのソリューションを開き [!INCLUDE[vs2010](../includes/vs2010-md.md)] 、**ソリューションエクスプローラー**でソリューションを右クリックして、[**追加**]、[**新しいプロジェクト...** ] の順に選択します。 を選択すると、[ **新しいプロジェクト** ] ダイアログボックスが開きます。 上記の手順を実行します。

8. プロジェクト テンプレートにより、アクティビティ デザイナー定義が XAML で作成され、ソース コード内に分離コード実装ファイルが作成されます。 [!INCLUDE[wfd1](../includes/wfd1-md.md)]で、アクティビティ デザイナー用のキャンバスが開かれて表示されます。

9. コントロールを [ [!INCLUDE[avalon1](../includes/avalon1-md.md)] **ツールボックス** ] からデザイン画面にドラッグして、カスタムアクティビティデザイナーで使用できるようにします。  カスタムアクティビティデザイナーを実装する方法の例については、「 [方法: カスタムアクティビティデザイナーを作成](https://msdn.microsoft.com/library/2f3aade6-facc-44ef-9657-a407ef8b9b31)する」を参照してください。

    > [!WARNING]
    > カスタムアクティビティデザイナーは、既定のアクティビティだけでなく、カスタムアクティビティにも使用でき [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] ます。

## <a name="see-also"></a>参照
 [ワークフロー プロジェクトの作成](../workflow-designer/creating-a-workflow-project.md)