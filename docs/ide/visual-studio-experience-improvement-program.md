---
title: カスタマー エクスペリエンス向上プログラム
description: Visual Studio でプライバシー設定を管理する方法を確認します。
ms.date: 05/21/2018
ms.topic: conceptual
author: PoulChapman
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 60a67da568703282a3ae469afa4dbc15c53cf4ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873945"
---
# <a name="visual-studio-customer-experience-improvement-program"></a>Visual Studio カスタマー エクスペリエンス向上プログラム

Visual Studio カスタマー エクスペリエンス向上プログラム (VSCEIP) は、Microsoft による Visual Studio の改善を時間の経過と共に支援するように設計されています。 このプログラムは、コンピューターでのユーザーのタスクを中断させずにコンピューター ハードウェア、ユーザーの Visual Studio の利用、[エラーに関する情報を収集](../ide/diagnostic-data-collection.md)します。 収集される情報は、Microsoft が改善する機能を特定するために役立ちます。 このドキュメントは、VSCEIP を有効または無効を選択する方法を説明します。

[!INCLUDE [gdpr-hybrid-note](../misc/includes/gdpr-hybrid-note.md)]
> [!NOTE]
> VSCEIP のテレメトリのオプトインまたはオプトアウトの設定は、Visual Studio の [問題の報告] には適用されません。 問題を報告するときに、[送信] をクリックしてアクセス許可を指定した場合にのみ、ログが収集され、Microsoft に送信されます。 [問題の報告] に送信する前にログの管理について確認する場合、詳細については、[データのプライバシーのフィードバック](./developer-community-privacy.md)に関する記事を参照してください。

## <a name="opt-in-or-out"></a>オプトインまたはオプトアウト

VSCEIP は既定で有効になっています。 次の手順で、オフにしたり、もう一度でオンにしたりできます。

1. Visual Studio で、 **[ヘルプ]**  >  **[フィードバックの送信]** を選択し、 **[設定]** を選択します。

   **[Visual Studio エクスペリエンス向上プログラム]** ダイアログ ボックスが開きます。

1. オプトアウトするには、**[いいえ、参加しません]** を選んでから、**[OK]** を選びます。 オプトインするには、**[参加する]** を選んでから、**[OK]** を選びます。

   ![[Visual Studio エクスペリエンス向上プログラム] ダイアログ](media/experience-improvement-program.png)

### <a name="registry-settings"></a>レジストリ設定

[Build Tools for Visual Studio](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2017) をインストールする場合は、レジストリを更新して VSCEIP を構成する必要があります。 企業のお客様の場合、レジストリ ベースのポリシーを設定することにより、VSCEIP を有効または無効にするグループ ポリシーを構成できます。

これに関連するレジストリ キーと設定は以下のとおりです。

::: moniker range="vs-2017"

- 64 ビット OS の場合: キー = **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM**
- 32 ビット OS の場合: キー = **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM**
- グループ ポリシーが有効になっている場合: キー = **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM**

::: moniker-end

::: moniker range=">=vs-2019"

- 64 ビット OS の場合: キー = **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\16.0\SQM**
- 32 ビット OS の場合: キー = **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\16.0\SQM**
- グループ ポリシーが有効になっている場合: キー = **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM**

::: moniker-end

エントリ = **OptIn**

値 = (DWORD)

- **0**: オプトアウト (VSCEIP をオフにする)
- **1**: オプトイン (VSCEIP をオンにする)

> [!CAUTION]
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。 手動での変更の適用後に問題が発生した場合は、 **[前回正常起動時の構成]** スタートアップ オプションを使うこともできます。

VSCEIP によって収集、処理、または送信される情報については、「[Microsoft のプライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」を参照してください。

## <a name="see-also"></a>関連項目

* [Visual Studio によって収集される診断情報](diagnostic-data-collection.md)
* [Visual Studio フィードバック オプション](../ide/feedback-options.md)
* [Visual Studio 2017 で問題を報告する方法](../ide/how-to-report-a-problem-with-visual-studio.md)
* [Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)
* [Microsoft プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)
