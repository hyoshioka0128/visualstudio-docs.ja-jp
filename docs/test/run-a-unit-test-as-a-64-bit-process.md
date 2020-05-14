---
title: 64 ビット プロセスとして単体テストを実行する
ms.date: 03/10/2020
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests, running
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: d6c6839f8c4702d88d1022116231c6f22b5dbf21
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79093910"
---
# <a name="run-a-unit-test-as-a-64-bit-process"></a>64 ビット プロセスとして単体テストを実行する

64 ビット コンピューターの場合、単体テストを実行し、64 ビット プロセスとしてコード カバレッジ情報を取得できます。

## <a name="to-run-a-unit-test-as-a-64-bit-process"></a>64 ビット プロセスとして単体テストを実行するには

1. コードまたはテストを 32 ビット/x86 としてコンパイルされたが、それを 64 ビット プロセスとして実行する場合、**任意の CPU** として再コンパイルします。

   ::: moniker range="vs-2017"
   あるいは、Visual Studio 2017 では **64 ビット**としてプロジェクトをコンパイルすることもできます。
   ::: moniker-end

    > [!TIP]
    > 柔軟性を最大限に高めるには、テスト プロジェクトを**任意の CPU** 構成でコンパイルします。 これにより、32 ビット エージェントと 64 ビット エージェントの両方で実行できます。 **64 ビット**構成でテスト プロジェクトをコンパイルしても、特に利点はありません。

2. 64 ビット プロセスとして実行されるように単体テストを設定します。

   ::: moniker range=">=vs-2019"
   Visual Studio メニューから、 **[テスト]** を選択し、 **[AnyCPU プロジェクトのプロセッサ アーキテクチャ]** を選択します。 64 ビット プロセスとしてテストを実行するには、 **[x64]** を選択します。
   ::: moniker-end
   ::: moniker range="vs-2017"
   Visual Studio メニューから、 **[テスト]** を選択し、 **[テストの設定]** を選択し、 **[プロセッサ アーキテクチャ]** を選択します。 64 ビット プロセスとしてテストを実行するには、 **[x64]** を選択します。
   ::: moniker-end

   \- または

   *.runsettings* ファイルに `<TargetPlatform>x64</TargetPlatform>` を指定します。 この方法の長所は、さまざまなファイルに設定のグループを指定し、設定を簡単に切り替えられることです。 ソリューション間で設定をコピーすることもできます。 詳細については、「[.runsettings ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)
- [コードの単体テスト](../test/unit-test-your-code.md)
