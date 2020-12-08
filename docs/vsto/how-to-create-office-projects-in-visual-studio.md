---
title: '方法: Visual Studio で Office プロジェクトを作成する'
description: Visual Studio を使用して、Microsoft Office アプリケーションの VSTO アドインとドキュメントレベルのカスタマイズを作成する方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.SelectDocWizard.Page1
- VST.SelectDocWizard.Http
- VST.SelectDocWizard.Extension
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], creating projects
- Office applications [Office development in Visual Studio], creating
- Office projects [Office development in Visual Studio]
- projects [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], creating projects
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 652b7676ddf5d7e095010e711ab0dabc5b5f2ab7
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96844375"
---
# <a name="how-to-create-office-projects-in-visual-studio"></a>方法: Visual Studio で Office プロジェクトを作成する
  を使用すると、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Microsoft Office アプリケーションの VSTO アドインとドキュメントレベルのカスタマイズを作成できます。 これらの種類のプロジェクトの詳細については、「 [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-a-vsto-add-in-project"></a>VSTO アドイン プロジェクトを作成するには

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。 統合開発環境 (IDE) が開発設定を使用するように設定されている場合は、[ [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] **ファイル**] メニューの [**新しい** プロジェクト] をクリックし  >  **Project** ます。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > 既定では、Office プロジェクトは [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とします。 詳細については、「 [.NET Framework client profile](/dotnet/framework/deployment/client-profile)」を参照してください。

2. [テンプレート] ウィンドウで、使用する言語のノードの下にある [ **Office/SharePoint**] を展開します。

3. [ **Office アドイン** ] ノードを選択します。

4. プロジェクト テンプレートの一覧で、VSTO アドイン プロジェクト テンプレートを選択します。 使用可能な VSTO アドインプロジェクトテンプレートの一覧については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

   > [!NOTE]
   > [ **Office アドイン** ] ノードを選択したときにプロジェクトテンプレートが表示されない場合は、ダイアログボックスの上部にあるコンボボックスで **.NET Framework 4** 以降が選択されていることを確認してください。 Office プロジェクト テンプレートは、.NET Framework の両方のバージョンで表示されます。

5. [ **名前** ] ボックスに、プロジェクトの名前を入力します。 既定では、このプロジェクト名がソリューション名としても使用されます。

6. [ **場所** ] ボックスに、プロジェクトを作成する場所のパスを入力します。 絶対パスと UNC (Universal Naming Convention) パスを使用できます。 HTTP、FTP、またはその他のプロトコル パスは使用しないでください。

    場所は、次の形式で指定します。

   * [*ドライブ*\]\:

   * \\\\*サーバー* \\*共有*

     次の文字は使用しないでください。

   * アスタリスク (*)

   * 縦棒 (|)

   * コロン (:) (ドライブ文字の後に使用する場合は除く)

   * 二重引用符 (") (スペースを含むパスには引用符は不要)

   * より小さい (\<)

   * より大きい (>)

   * 疑問符 (?)

   * パーセント記号 (%)

7. **[OK]** を選択します。

   ::: moniker range="vs-2017"

   > [!NOTE]
   > アドイン プロジェクトを作成すると、必ず保存されます。 アドイン プロジェクトを一時プロジェクトとして作成することはできません。 一時プロジェクトの詳細については、「 [一時プロジェクト](../ide/creating-solutions-and-projects.md#create-a-temporary-project)」を参照してください。

   ::: moniker-end

### <a name="to-create-a-document-level-customization-project"></a>ドキュメント レベルのカスタマイズ プロジェクトを作成するには

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、[**ファイル**] メニューの [**新しい** プロジェクト] をクリックし  >  **Project** ます。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [テンプレート] ウィンドウで、使用する言語のノードの下にある [ **Office/SharePoint**] を展開します。

3. **[Office アドイン]** ノードを選択します。

4. プロジェクト テンプレートの一覧で、ドキュメント レベルのプロジェクト テンプレートを選択します。 使用できるドキュメントレベルのプロジェクトテンプレートの一覧については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

   > [!NOTE]
   > [ **Office アドイン** ] ノードを選択したときにプロジェクトテンプレートが表示されない場合は、 **.NET Framework 4** 以降が選択されていることを確認してください。

5. [ **名前** ] ボックスに、プロジェクトの名前を入力します。 既定では、この名前がドキュメントにも使用されます。 IDE が Visual C# 開発設定または一般的な開発設定を使用するように設定されている場合は、場所とソリューション名も入力します。

   > [!NOTE]
   > プロジェクトの場所へのパス、またはプロジェクト名には、サロゲート文字を使用できません。 また、オフラインで使用するソリューションを配置する場合は、プロジェクト名に HTTP プロトコルの仕様に準拠した文字を使用する必要があります。

6. **[OK]** を選択します。

    **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

7. ソリューションの新しいドキュメントを作成する場合は [ **新しいドキュメントを作成** する] を選択し、既存のドキュメントをカスタマイズする場合は [ **既存のドキュメントをコピー** する] を選択します。

    新しいドキュメントを作成する場合は、[ **名前** ] ボックスに名前を指定し、[ **書式** ] ボックスを使用してドキュメントの形式を選択します。 使用可能な形式の詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

    既存のドキュメントを使用する場合は、 **既存のドキュメントボックスの完全パス** にドキュメントの場所を指定します。 使用できるパスは、絶対パスと UNC パスです。 ドキュメントへの HTTP パス、FTP パス、または他のプロトコル パスは使用しないでください。

    場所は、次の形式で指定します。

   - [*ドライブ*\]\:

   - \\\\*サーバー* \\*共有*

     次の文字は使用しないでください。

   - アスタリスク (*)

   - 縦棒 (|)

   - コロン (:) (ドライブ文字の後に使用する場合は除く)

   - 二重引用符 (") (スペースを含むパスには引用符は不要)

   - より小さい (\<)

   - より大きい (>)

   - 疑問符 (?)

   - パーセント記号 (%)

   > [!NOTE]
   > [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] プロジェクトで既存のドキュメントを使用する場合は、[!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] で作成したドキュメントか、この形式に変換したドキュメントだけを使用してください。 同様に、Word 2010 プロジェクトで既存のドキュメントを使用する場合は、Word 2010 で作成したドキュメントか、Word 2010 に変換したドキュメントだけを使用してください。 以前のバージョンの Word で作成した文書を使用すると、文書の一部の機能が使用できなくなります。 このような機能を使用するコードを記述しようとすると、プロジェクトでエラーが発生する可能性があります。 ドキュメントを変換するには、または Word 2010 でドキュメントを開き、 [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] リボンの [**ファイル**] タブで [**情報** 変換] を選択し  >  **Convert** ます。

8. **[完了]** を選択します。

9. 次の場合、Word のセキュリティ センターにある信頼できる場所の一覧に、プロジェクト フォルダーとそのサブフォルダーを追加します。

   - *.Docm* ファイルに基づく Word 文書を作成し、ドキュメントに VBA プロジェクトが含まれているか Windows フォームコントロールをホストしています。 プロジェクト フォルダーを信頼できる場所の一覧に追加すると、デザイン時に文書が期待どおりに動作するか確認するのに役立ちます。

   - *.Dotx* ファイルに基づく Word テンプレートプロジェクトを作成する場合。 プロジェクトを実行およびデバッグできるようにするために、プロジェクト フォルダーを信頼できる場所の一覧に追加する必要があります。

     信頼できる場所にドキュメントを追加する方法の詳細については、Microsoft Office オンライン web サイト「 [ファイルの信頼できる場所を作成、削除、または変更](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)する」を参照してください。

## <a name="see-also"></a>関連項目
- [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)
- [Office ソリューションの共同開発](../vsto/collaborative-development-of-office-solutions.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
