---
title: 単体テスト プロジェクトを作成する
ms.date: 01/29/2019
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 313083090c94c94f4e196e87f3bf6cf6df36e118
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75565254"
---
# <a name="create-a-unit-test-project"></a>単体テスト プロジェクトを作成する

単体テストでは、多くの場合、テスト対象のコードの構造を再現します。 たとえば、製品のコード プロジェクトごとに単体テスト プロジェクトを作成します。 テスト プロジェクトは本稼働コードと同じソリューションに置くことも、別個のソリューションに置くこともできます。 1 つのソリューションに複数の単体テスト プロジェクトを置くこともできます。

> [!NOTE]
> ネイティブ コードの単体テストの場所とテスト プロジェクトの構造は、この記事の説明にある構造とは異なっていても構いません。 詳細については、「[C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)」を参照してください。

## <a name="to-create-a-unit-test-project"></a>単体テスト プロジェクトを作成するには

1. **[ファイル]** メニューで、 **[新規作成]**  >  **[プロジェクト]** の順に選択するか、または **Ctrl**+**Shift**+**N** キーを押します。

::: moniker range="vs-2017"

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストール済み]** ノードを展開して、テスト プロジェクトで使用する言語を選択し、 **[テスト]** をクリックします。

3. 使用するテスト フレームワークのプロジェクト テンプレートを選択します (**MSTest テスト プロジェクト**や **NUnit テスト プロジェクト**など)。 プロジェクトに名前を付けて、 **[OK]** を選択します。

   ![Visual Studio 2017 でのテスト プロジェクト テンプレート](media/test-project-templates.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**単体テスト**」と入力します。 使用するテスト フレームワークのプロジェクト テンプレート (**MSTest テスト プロジェクト**や **NUnit テスト プロジェクト**など) を選択して、 **[次へ]** をクリックします。

   ![Visual Studio 2019 でのテスト プロジェクト テンプレート](media/vs-2019/test-project-templates.png)

3. **[新しいプロジェクトの構成]** ページで、ご自分のプロジェクトの名前を入力して、 **[作成]** を選択します。

::: moniker-end

4. 単体テスト プロジェクトに、テスト対象のコードへの参照を追加します。 同じソリューション内のコード プロジェクトへの参照を追加するには:

   1. **ソリューション エクスプローラー**でテスト プロジェクトを選択します。

   2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

   3. **[参照マネージャー]** で、 **[プロジェクト]** の下の **[ソリューション]** ノードを選択します。 テストするコード プロジェクトを選択して、 **[OK]** を選択します。

   テストするコードが別の場所にある場合は、「[プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

次のいずれかのセクションを参照してください。

**単体テストの記述**

- [コードの単体テスト](../test/unit-test-your-code.md)

- [C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)

- [単体テストでの MSTest フレームワークの使用](using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md)

**単体テストの実行**

- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)
