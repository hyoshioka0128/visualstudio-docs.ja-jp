---
title: IntelliTrace データ
description: Visual Studio で、IntelliTrace の診断データ アダプターを構成して、特定の診断トレース情報を収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/13/2016
ms.topic: how-to
helpviewer_keywords:
- IntelliTrace, configuring test settings
- Diagnostic Data Adapter, InteliTrace
- debugging [Visual Studio ALM], difficult issues using IntelliTrace
- Test Runner, InteliTrace
ms.assetid: 02b6716f-569e-4961-938a-e790a0c74b5c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a043f2841dc5a6918036c152628ebfc346e11ee
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95440109"
---
# <a name="how-to-collect-intellitrace-data-to-help-debug-difficult-issues"></a>方法: 困難な問題をデバッグするのに役立つ IntelliTrace データを収集する

Visual Studio では、特定の診断トレース情報を収集するように IntelliTrace の診断データ アダプターを構成できます。 テストではこのアダプターを使用できます。またテストではアプリケーションの重要な診断イベントを収集できます。これを使用して開発者はコードを追跡し、バグの原因を見つけることができます。 IntelliTrace の診断データ アダプターは、手動テストでも自動テストでも使用できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> IntelliTrace はマネージド コードで作成されたアプリケーションでのみ機能します。 ブラウザーをクライアントとして使用する Web アプリケーションをテストしている場合は、トレースするマネージド コードがないので、テストの設定でクライアントに対して IntelliTrace を有効にしないでください。 この場合は、環境を設定し、Web サーバーで IntelliTrace データをリモートで収集できます。

IntelliTrace データは、拡張子が *.iTrace* のファイルに保存されます。 テストを実行し、テスト ステップが失敗した場合は、バグを作成できます。 診断情報が格納された IntelliTrace ファイルは、このバグに自動的にアタッチされます。

> [!NOTE]
> テストが成功した場合、IntelliTrace の診断データ アダプターで IntelliTrace ファイルは作成されません。 テスト ケースが失敗した場合、またはバグを送信した場合にのみファイルが保存されます。

IntelliTrace ファイルに収集されたデータによって、コードのエラーを再現して診断するために必要な時間が短縮され、この結果、デバッグの生産性が向上します。 また、ローカル セッションを自分のコンピューターで複製できる他のユーザーと IntelliTrace ファイルを共有できるので、バグが再現不可能となる可能性が低くなります。

> [!NOTE]
> テストの設定で IntelliTrace を有効にすると、コード カバレッジ データの収集は実行されません。

> [!WARNING]
> IntelliTrace の診断データ アダプターは、マネージド プロセスをインストルメント化することで機能しますが、これは、実行するテストが読み込まれた後に行われる必要があります。 監視するプロセスが既に開始されている場合、プロセスは既に実行中であるため、IntelliTrace ファイルは収集されません。 これを回避するため、テストを読み込む前に必ずプロセスを停止してください。 テストが読み込まれた後、または最初のテストが開始された後でプロセスを開始します。

::: moniker range="vs-2017"
次の手順では、収集する IntelliTrace データを構成する方法を説明します。 これらの手順は Microsoft Test Manager の構成エディターと Visual Studio の [テストの設定] ダイアログ ボックスの両方に当てはまります。
::: moniker-end
::: moniker range=">=vs-2019"
次の手順では、収集する IntelliTrace データを構成する方法を説明します。 これらの手順は、Visual Studio の [テストの設定] ダイアログ ボックスに当てはまります。
::: moniker-end

> [!NOTE]
> IntelliTrace データの収集に使用されるテスト エージェントのユーザー アカウントは、Administrators グループのメンバーである必要があります。 詳細については、[テスト エージェントのインストールと構成](../test/lab-management/install-configure-test-agents.md)に関するページを参照してください。

## <a name="configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>IntelliTrace 診断データ アダプターで収集するデータの構成

::: moniker range="vs-2017"
この手順を実行する前に、Microsoft Test Manager または Visual Studio からテストの設定を開き、 **[データと診断]** ページを選択する必要があります。
::: moniker-end
::: moniker range=">=vs-2019"
この手順を実行する前に、Visual Studio からテストの設定を開き、 **[データと診断]** ページを選択する必要があります。
::: moniker-end

### <a name="to-configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>IntelliTrace 診断データ アダプターで収集するデータを構成するには

1. IntelliTrace データの収集に使用するロールを選択します。

2. **[IntelliTrace]** を選択します。

3. Web クライアント ロールまたは ASP.NET Web アプリケーションに IntelliTrace を追加している場合は、 **[IntelliTrace およびテストの影響用の ASP.NET クライアント プロキシ]** を選択する必要もあります。

     このプロキシを使用すると、IntelliTrace 診断データ アダプターとテスト影響診断データ アダプターでクライアントから Web サーバーへの http 呼び出しに関する情報を収集できます。

    > [!WARNING]
    > IntelliTrace データを収集する Internet Information Server (IIS) のアプリケーション プールで使用されている ID のカスタム アカウントを使用する場合、IIS コンピューター上で使用するカスタム アカウントのローカル ユーザー プロファイルを作成する必要があります。 カスタム アカウントのローカル プロファイルを作成するには、IIS コンピューターに一度ローカルでログインするか、カスタム アカウントの資格情報を使用して以下のコマンド ラインを実行します。
    >
    > **runas /user:domain\name /profile cmd.exe**

4. **[IntelliTrace]** の **[構成]** を選択し、既定の IntelliTrace 設定を変更します。

     収集されるデータを構成するダイアログ ボックスが表示されます。

    > [!WARNING]
    > IntelliTrace データの収集を有効にすると、コード カバレッジ データの収集は実行されません。

5. **[全般]** タブを選択します。重要な診断イベントを記録する場合に **[IntelliTrace イベントのみ]** を選択すると、テスト時のパフォーマンスへの影響を最小限に抑えられます。

     \- または -

     診断イベントと、呼び出し情報を示すメソッド レベルのトレースを記録する場合は、 **[IntelliTrace イベントと呼び出し情報]** を選択します。 このレベルのトレースは、テストの実行時のパフォーマンスに影響を与えます。

6. インターネット インフォメーション サービスで実行されている ASP.NET アプリケーションからデータを収集するには、 **[インターネット インフォメーション サービスで実行されている ASP.NET アプリケーションからデータを収集する]** を選択します。 Web サーバー ロールにテスト エージェントを設定して構成します。 「[テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)」を参照してください。

7. **[モジュール]** タブを選択します。 **[次を除くすべてのモジュールからデータを収集]** を選択し、 **[追加]** をクリックしてモジュールのリストに追加するか、 **[削除]** をクリックしてモジュールを削除します。 このオプションを選択すると、指定したモジュールを除く、システムで実行されているすべてのモジュールがデータ収集の対象となります。

     \- または -

     **[次のモジュールからのみデータを収集]** を選択し、 **[追加]** をクリックしてモジュールのリストに追加するか、 **[削除]** をクリックしてモジュールを削除します。 このオプションを選択すると、必要なモジュールを正確に指定できます。

    > [!NOTE]
    > 可能な場合、監視対象として特定のプロセスを選択します。 パフォーマンスを最適化するためには、この方法をお勧めします。

8. **[プロセス]** タブを選択します。 **[次を除くすべてのプロセスからデータを収集]** を選択し、 **[追加]** をクリックしてプロセスのリストに追加するか、 **[削除]** をクリックしてプロセスを削除します。 このオプションを選択すると、指定したプロセスを除く、システムで実行されているすべてのプロセスがデータ収集の対象となります。

     \- または -

     **[指定されたプロセスからのみデータを収集]** を選択し、 **[追加]** をクリックしてプロセスのリストに追加するか、 **[削除]** をクリックしてプロセスを削除します。 このオプションを選択すると、必要なプロセスを正確に指定できます。

9. (省略可能) **[IntelliTrace イベント]** タブを選択します。診断イベントを収集するときに含める各 IntelliTrace イベント カテゴリを選択するか、除外する各 IntelliTrace イベント カテゴリをクリアします。

10. (省略可能) 各 IntelliTrace イベント カテゴリを展開し、IntelliTrace イベントに含めるか、IntelliTrace イベントから除外する特定のイベントをそれぞれ選択またはクリアします。

11. (省略可能) **[詳細]** タブをクリックします。次に、 **[各記録用の最大ディスク領域]** の横にある矢印を選択し、使用する IntelliTrace ファイルで許可する最大サイズを選択します。

    > [!NOTE]
    > 記録のサイズを大きくすると、記録をテスト結果と共に保存するときタイムアウトが発生する可能性があります。

12. Microsoft Test Manager (Visual Studio 2017 では非推奨) を使用している場合は、 **[保存]** を選択します。 Visual Studio を使用している場合は、 **[OK]** をクリックします。 これで、テストの設定を対象として IntelliTrace の設定が構成および保存されました。

    ::: moniker range="vs-2017"
    > [!NOTE]
    > この診断データ アダプターの構成をリセットするには、Visual Studio の場合は **[既定の構成にリセット]** をクリックし、Microsoft Test Manager の場合は **[既定値にリセット]** をクリックします。
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    > [!NOTE]
    > この診断データ アダプターの構成をリセットするには、Visual Studio で **[既定の構成にリセット]** をクリックします。
    ::: moniker-end

## <a name="see-also"></a>関連項目

- [テスト中の診断データの収集 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts&preserve-view=true)
- [手動テストでの診断データの収集 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts&preserve-view=true)
- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)
- [IntelliTrace データの収集](../test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md)
