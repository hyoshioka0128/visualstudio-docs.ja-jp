---
title: '方法: ワークフローコンソールアプリケーションを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 51a2eea7-921c-49f1-b358-68afc27f1ee9
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1334655f2a8b8587922628664e43784b54ce971
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72604920"
---
# <a name="how-to-create-a-workflow-console-application"></a>ワークフロー コンソール アプリケーションを作成する方法
[!INCLUDE[wf](../includes/wf-md.md)] システムまたはヒューマンプロセスを実行するためのワークフローを作成できます。 [!INCLUDE[wfd1](../includes/wfd1-md.md)]は、このようなワークフローを作成するためのデザイン サーフェイスを備えています。 [!INCLUDE[wfd2](../includes/wfd2-md.md)]は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内からワークフローを作成する場合に使用でき、デザイナーを再ホストする他のアプリケーションに統合することもできます。

 このトピックでは、[!INCLUDE[wfd2](../includes/wfd2-md.md)] の[!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用して、コンソール アプリケーションのワークフローを作成する方法について説明します。

### <a name="to-create-a-workflow-console-application"></a>ワークフロー コンソール アプリケーションを作成するには

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)]を起動します。

2. [ **ファイル** ] メニューの [ **新規作成**] をポイントし、[ **プロジェクト**] をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. [**インストールされたテンプレート**] ペインで、好みの言語に応じて、 **Visual C#** または**Visual Basic**グループのいずれかから [**ワークフロー** ] を選択します。

4. 中央のペインで、[ **ワークフローコンソールアプリケーション**] を選択します。

5. [ **名前** ] ボックスに、プロジェクトのわかりやすい名前を入力します。

6. [ **場所** ] ボックスに、プロジェクトを保存するディレクトリを入力するか、[ **参照** ] をクリックして移動します。

7. [ **ソリューション** ] ボックスに、新しいソリューションの名前を入力します。 [ **OK** ] をクリックしてアプリケーションを作成します。

    > [!NOTE]
    > ワークフローコンソールアプリケーションを既存のソリューションに追加する場合は、でそのソリューションを開き [!INCLUDE[vs2010](../includes/vs2010-md.md)] 、**ソリューションエクスプローラー**でソリューションを右クリックして、[**追加**]、[**新しいプロジェクト...** ] の順に選択します。 を選択すると、[ **新しいプロジェクト** ] ダイアログボックスが開きます。 上記の手順を実行します。

8. プロジェクト テンプレートで XAML のワークフロー定義が作成され、コンソール アプリケーション定義がソース コードに記述されます。 [!INCLUDE[wfd2](../includes/wfd2-md.md)]で、作成したワークフロー用のキャンバスが開かれて表示されます。

9. ワークフローを作成するには、アクティビティまたはその他のワークフロー項目を、 **ツールボックス** からワークフローのデザイン画面にドラッグします。

## <a name="see-also"></a>参照
 [ワークフロー プロジェクトの作成](../workflow-designer/creating-a-workflow-project.md)