---
title: Microsoft Language Interface Pack (LIP) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- text [Visual Studio], multiple languages
- Multilingual User Interface [Visual Studio]
- language switching [Visual Studio]
- MUI [Visual Studio]
- multiple language support [Visual Studio SDK]
- Windows Multilingual User Interface
- UI text language [Visual Studio]
- languages, multiple language support
ms.assetid: dc86304b-65b7-47e6-9314-1dfd02ecfa65
caps.latest.revision: 28
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 503f97d1530f8d22184f42a2452046782a997c18
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432995"
---
# <a name="microsoft-language-interface-packs-lips-and-visual-studio"></a>Microsoft Language Interface Pack (LIP) および Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Language Interface Pack (LIP) を使用すると、1 つの言語バージョンの Windows をインストールし、次にさまざまな User Interface Language Pack をインストールできます。 User Interface Language Pack には、オペレーティング システムのローカライズされたユーザー インターフェイス (UI) が用意されています。 たとえば、英語バージョンの Windows に日本語の Language Interface Pack をインストールし、Windows の UI 言語を日本語と英語で切り替えることができます。 LIP を使用すると、複数の言語バージョンの Windows を 1 台のコンピューターで使用できます。

 Visual Studio の LIP と複数の言語バージョンがインストールされたコンピューターでは、一致する Language Pack がインストールされている場合に、Windows の表示言語を変更すると Windows と Visual Studio の両方が設定されます。

## <a name="limitations-of-multi-language-installations"></a>複数言語インストールでの制限
 言語バージョンが異なる Visual Studio を同じコンピューターにインストールする場合、一致するエディションの間のみで言語を切り替えることができます。 たとえば、英語バージョンの Express Edition、ドイツ語バージョンの Express Edition、および Professional Edition がそれぞれインストールされている場合、言語を切り替えできるのは Express Edition だけで、Professional Edition の言語は切り替えできません。

 Visual Studio は、統一された言語パックを使用します。 これらの製品の複数の言語バージョンをインストールするには、最初に 1 つの言語の製品版をインストールしてから、1 つ以上の Language Pack をインストールする必要があります。

> [!NOTE]
> Visual Studio では、同じコンピューターへの複数言語バージョンの製品版のインストールをサポートしていません。 1 つの言語の製品版をインストールしたら、Language Pack を使用して言語バージョンを追加する必要があります。 Express Edition の場合は、これまでどおり複数の言語の製品版を同じコンピューターにインストールできます。

### <a name="support-for-code-pages"></a>コード ページのサポート
 Visual Studio Tools によっては、現在のコード ページではない文字がテキストに含まれるときに、そのテキストを正しく表示できません。 その代わりに疑問符が表示されるか、テキストが破損します。 次のツールまたは分野に影響があります。

- FTP を使用して配置されるサイト。

- 一部のコントロールでの ASCII 以外のコンピューター名。

- Visual Studio の外部で実行されるコマンド ライン ツール。

- Visual Basic 移行ウィザード。

- ActiveX コントロール テスト コンテナー。

- OLE/COM オブジェクト ビューアー。

- ISAPI Web デバッグ ツール。

- HTML ヘルプ コンテンツを持つ MFC アプリケーション プロジェクト。

- Visual SourceSafe / SCCI の UI は、互換性のないコード ページがある場合は、英語に戻ります。

- Visual SourceSafe は Unicode のファイル名をサポートしません。

- エンド ユーザー定義の文字 (個人用領域) をトークンまたは識別子として使用できません。

- Windows コード ページが東アジア言語に設定されている場合、一部の Visual Studio ツール ウィンドウでラテン拡張文字 B を表示できません。

- 複数言語の文字で構成されたテキストで、一部の文字に対して既定のグリフが表示される場合があります。

- 共通のコントロールに複雑な文字を使用した文字列をコピーして貼り付けると、文字の形状が失われる場合があります。 代わりに、対応する言語のキーボードを使用してテキストを入力します。

##### <a name="to-correctly-display-characters-that-are-not-included-in-the-current-code-page"></a>現在のコード ページに含まれない文字を正しく表示するには

1. **[スタート]** ボタン、**[コントロール パネル]**、**[地域と言語のオプション]** ([!INCLUDE[win8](../includes/win8-md.md)] では **[領域]**) の順にクリックします。

    > [!NOTE]
    > 次の手順を実行するには、そのコンピューターの管理者である必要があります。

2. **[詳細設定]** タブをクリックします。

3. **[使う Unicode 対応でないプログラムの言語バージョンに一致する言語を選んでください]** の一覧で、現在使用している言語を選択します。

4. **[OK]** をクリックします。

## <a name="changing-the-language-used-for-the-ui-text-in-visual-studio"></a>Visual Studio の UI テキストに使用される言語の変更
 同じコンピューターに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の複数の言語バージョンをインストールすると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の UI は既定で **[Microsoft Windows と同じ]** になります。 この設定は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がオペレーティング システムの表示言語として指定された言語の UI テキストを表示することを示しています。

> [!NOTE]
> Visual Studio が **[Microsoft Windows と同じ]** を使用するように設定され、一致する Visual Studio の Language Pack がインストールされていない場合、Visual Studio は最初の Visual Studio インストールの言語を使用します。

#### <a name="to-set-the-language-that-is-used-for-the-ui-text-in-visual-studio"></a>Visual Studio の UI テキストに使用される言語を設定するには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスの **[環境]** を展開し、**[国際対応の設定]** をクリックします。

3. **[言語]** ボックスの一覧で、開発環境における UI テキストの表示言語を選択します。

    IDE の UI テキストをオペレーティング システムの表示言語設定と一致させるには、**[Microsoft Windows と同じ]** を選択します。

   また、devenv コマンドを使用して、UI に使用される言語を設定することもできます。 詳細については、「[/lcid (devenv.exe)](../ide/reference/lcid-devenv-exe.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [[国際対応の設定] ([オプション] ダイアログ ボックス - [環境])](../ide/reference/international-settings-environment-options-dialog-box.md)
