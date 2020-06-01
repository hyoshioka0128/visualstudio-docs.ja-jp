---
title: Visual Studio サブスクリプションを割り当てるにはどうすればよいですか?
description: エンド ユーザーにサブスクリプションを一度に 1 つずつ割り当てることも、一括追加機能を使用して、すばやく簡単に多数の...をアップロードすることもできます
ms.faqid: group1_3
ms.topic: include
ms.assetid: 59eb35fd-ec94-41ce-b24c-a8a120976bac
author: CaityBuschlen
ms.author: cabuschl
ms.date: 3/3/2020
ms.openlocfilehash: 192cb7118a9f431ce2e7a9396b67a919fad10bb9
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84200540"
---
## <a name="how-do-i-assign-visual-studio-subscriptions"></a>Visual Studio サブスクリプションを割り当てるにはどうすればよいですか?

エンド ユーザーにサブスクリプションを一度に 1 つずつ割り当てることも、一括追加機能を使用して、すばやく簡単に多数のサブスクライバーを一度にアップロードすることもできます。

サブスクリプションを個別に割り当てるには:

1. [manage.visualstudio.com](https://manage.visualstudio.com) のページの上部にある [[サブスクライバーを管理] タブ](https://manage.visualstudio.com/subscribers)を選択します
2. [追加] を選択し、サブスクリプションを割り当てるユーザーの名前とメール アドレスを入力します。
    1. 組織で Azure Active Directory を使用している場合は、名前フィールドによって、現在のディレクトリ内のユーザーが検索されます。 検索結果から選択することも、手動でユーザーを追加することもできます。
3. サブスクライバーが [Visual Studio サブスクリプション ポータル](https://my.visualstudio.com/)にサインインするときにソフトウェアのダウンロードにアクセスできるようにする場合は、必ず、[ダウンロードの設定] セクションのダウンロードのトグルをオンのままにしてください。
4. [通信設定] セクションに入力し、サブスクライバーに割り当てメールを送信する際の言語がわかるようにします。
5. 割り当てに関連付けられるメモを追加する場合は、参照選択を使用してください。
6. フライアウト パネルの下部にある [追加] を選択して、サブスクリプションの割り当てを完了します。 サブスクライバーはメールを受信し、すぐに Visual Studio サブスクリプションを使用し始めることができます (サブスクライバーがアクティブ化する必要はありません)。

サブスクリプションを一括で割り当てるには:

1. [manage.visualstudio.com](https://manage.visualstudio.com) のページの上部にある [[サブスクライバーを管理] タブ](https://manage.visualstudio.com/subscribers)を選択します。
2. [一括追加] を選択し、Excel テンプレートをダウンロードして、ローカル コピーを保存します。
3. [参照] フィールドを除く、すべてのフィールドに入力してください。
    1. フォームのどのフィールドにもコンマが含まれていないことを確認します。
    2. フォームのフィールドの前後のスペースを削除します。
    3. 名前の名または姓が 2 つの部分からなる場合、それらの間に余分なスペースがないようにしてください (たとえば、ユーザーの名が "Maggie May" のように 2 つの部分からなる場合は、"MaggieMay" と入力する必要があります)。
4. [manage.visualstudio.com](https://manage.visualstudio.com) に戻り、[一括追加] を選択して、保存した Excel テンプレートのコピーをアップロードします。
5. アップロードに成功すると、確認ページが表示され、新しいサブスクライバーが設定されたサブスクライバーの一覧が示されます。 サブスクライバーはメールを受信し、すぐに Visual Studio サブスクリプションを使用し始めることができます (サブスクライバーがアクティブ化する必要はありません)。

サブスクリプションをすばやく簡単に割り当てる方法の詳細については、[Visual Studio サブスクリプション管理者ポータルでのサブスクリプションの割り当て](https://docs.microsoft.com/visualstudio/subscriptions/assign-license#individual-assignments)に関するページを参照してください。
