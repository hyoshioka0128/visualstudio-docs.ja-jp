---
title: CPU カウンターと Windows カウンター | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.counters
helpviewer_keywords:
- Windows counters in Profiling Tools
- CPU counters in Profiling Tools
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9accd3d0ab5ff1f7a3084d5973cace08e66396b9
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779551"
---
# <a name="cpu-and-windows-counters"></a>CPU カウンターと Windows カウンター

Visual Studio プロファイラーでは、オペレーティング システムによって生成されたパフォーマンス データ (Windows カウンター) とプロセッサ ユニットによって生成されたパフォーマンス データ (CPU カウンター) を収集することができます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="windows-counters"></a>Windows カウンター

Windows カウンターは、オペレーティング システムまたはアプリケーション、サービス、ドライバーのパフォーマンスに関する情報を提供する Windows 診断インフラストラクチャの一部です。 Windows カウンターは、現在のコンピューターの構成に依存しており、他のコンピューターでは使用できない場合があります。 Windows パフォーマンス カウンターは、プロファイル マークとしてプロファイル データ ファイルに収集され、ビューおよびレポートのフィルター処理に使用できます。

## <a name="cpu-counters"></a>CPU カウンター

CPU カウンターは、ハードウェア関連のイベントの数を格納するコンピューターの CPU の機能です。 インストルメンテーション プロファイル メソッドを使用して CPU カウンター データを収集したデータは、関数およびモジュールのデータの後に追加されます。 インストルメンテーション メソッドを使用して複数の CPU カウンターを収集できます。 サンプリング メソッドを使用するときは、サンプリングされるイベントとして使用する 1 つのカウンターを選択します。

パフォーマンス カウンターは CPU 固有です。 CPU のモデルとバージョンが異なると、同じパフォーマンス カウンターを有効にする場合でも構成設定が大幅に異なることがあります。 [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] プロファイラーのポータブル イベントは、特定のプロセッサからよく使われる一部のパフォーマンス カウンターを分離し、汎用のパフォーマンス イベントを収集またはサンプリングできるようにします。

プロファイラーを使用するときに特定のイベント (たとえば、L2 キャッシュ ミス) をカウントしたい場合は、そのイベント送信元にパフォーマンス セッションを作成できます。 L2 キャッシュのある任意の CPU でこれを行うことができます。 パフォーマンス セッションは、変更することなく異なるプラットフォームに移動できます。

Visual Studio プロファイラーは、特定のプラットフォームの特定のイベントを継続してサポートします。 たとえば、Pentium 4 プラットフォームの開発者が NetBurst アーキテクチャに固有のイベントをカウントしたいものとします。 このイベントは移植可能ではありませんが、それでも特定のプラットフォームの特定のパフォーマンス セッションに対して使用できます。

## <a name="portable-and-platform-events"></a>ポータブル イベントとプラットフォーム イベント

ポータブル イベントとは、特定のプロセッサに固有ではない CPU カウンターのグループです。 他のすべての CPU カウンターはプラットフォーム イベントと呼ばれ、さまざまなプラットフォームでサポートされていない可能性があります。

 ポータブル イベントとプラットフォーム イベント両方のカウンターは *.xml* ファイルで定義されており、カウンターに関連する特定の値が提供されます。 たとえば Intel と AMD の CPU ではデータが異なるので、異なる CPU ごとに複数のファイルがあります。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] プロファイラーは、この情報を使用して、ポータブルとプラットフォーム両方の適切なカウンターを、パフォーマンス測定用にユーザーに提示します。

### <a name="portable-events"></a>Portable Events

ポータブル イベントには次のイベントが含まれます。

**一般イベント**

|イベント名|イベントの説明|
|----------------|-----------------------|
|Instructions Retired|イベントが完了するまで実行された命令の数を示します。|
|Non Halted Cycles|たとえば I/O の待機などでプロセッサが停止されなかったサイクルのみを示します。|

**フロント エンド イベント**

|イベント名|イベントの説明|
|----------------|-----------------------|
|ITLB Misses|ミスになった Instruction Translation Look-aside Buffer 参照の数を示します。|

**分岐イベント**

|イベント名|イベントの説明|
|----------------|-----------------------|
|Branches Retired|イベントが完了するまで実行された分岐命令の数を示します。|
|Mis-predicted Branches|プロセッサが正しくないパスを予測したために発生した誤予測分岐を示します。 誤予測分岐は、プロセッサが実行されたすべての処理を破棄して正しいパスで再度開始する必要があるため、パフォーマンスに影響します。|

**メモリ イベント:**

|イベント名|イベントの説明|
|----------------|-----------------------|
|L2 Cache Read Misses|第 2 レベルのキャッシュ読み取りミスの数を示します。|
|L2 Cache Read References|第 2 レベルのキャッシュ読み取り参照の数を示します。 読み込みミスおよび RFO (read for ownership) のミスとヒットを含みます。|

## <a name="view-available-counters"></a>使用可能なカウンターの表示

Visual Studio IDE またはコマンド プロンプト ウィンドウで、使用可能な CPU カウンターを一覧表示できます。

### <a name="visual-studio-ui"></a>Visual Studio UI

Visual Studio IDE でコンピューターの使用可能なカウンターを一覧表示するには、パフォーマンス エクスプローラーでプロファイラー パフォーマンス セッションを開いておく必要があります。

#### <a name="to-view-a-list-of-a-list-of-all-cpu-counters-that-are-supported-on-the-current-platform"></a>現在のプラットフォームでサポートされているすべての CPU カウンターの一覧を表示するには

1. パフォーマンス エクスプローラーで、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. 次のいずれかの操作を行います。

   - **[サンプリング]** をクリックし、 **[サンプル]** イベントの一覧から **[パフォーマンス カウンター]** を選びます。 **[使用可能なパフォーマンス カウンター]** に CPU カウンターが一覧表示されます。

      **注** 前のサンプリング構成に戻るには、 **[キャンセル]** をクリックします。

     または

   - **[CPU カウンター]** を選び、 **[CPU カウンターの収集]** を選びます。 **[使用可能なカウンター]** に CPU カウンターが一覧表示されます。

      **注** 前のカウンター収集構成に戻るには、 **[キャンセル]** をクリックします。

#### <a name="to-view-a-list-of-a-list-of-window-counters-that-are-supported-on-the-current-platform"></a>現在のプラットフォームでサポートされている Windows カウンターの一覧を表示するには

1. パフォーマンス エクスプローラーで、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[Windows カウンター]** をクリックします。

3. **[Windows カウンターの収集]** を選びます。

4. **[カウンター カテゴリ]** の一覧で、カウンター グループを選びます。 グループの Windows カウンターが、リスト ボックスに表示されます。

     **注:** 前のカウンター収集構成に戻るには、 **[キャンセル]** をクリックします。

### <a name="command-line"></a>コマンド ライン

[VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールを使って、コンピューターで使用可能な CPU カウンターを一覧表示できます。

#### <a name="to-list-of-cpu-counters-that-are-supported-on-the-current-platform"></a>現在のプラットフォームでサポートされている CPU カウンターの一覧を表示するには

1. コマンド プロンプト ウィンドウを開きます。

2. 型

     「 **\<Visual Studio パフォーマンス ツール ディレクトリ>\VSPerfCmd /querycounters**」と入力します。

     ここで、\<*Visual Studio パフォーマンス ツール ディレクトリ*> は、Visual Studio インストールのパフォーマンス ツール ディレクトリへのパスです。 パフォーマンス ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

[概要](../profiling/overviews-performance-tools.md)
[方法: サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)
[方法: CPU カウンター データを収集する](../profiling/how-to-collect-cpu-counter-data.md)
[方法: Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)
