---
title: ツールボックス、[コンポーネント] タブ
description: '[ツールボックス] ウィンドウの [コンポーネント] タブに含まれるコンポーネントについて説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CHOOSEITEMS.FrameworkComponents
- VS.CHOOSEITEMS.COMComponents
- VS.CHOOSEITEMS.UniversalWindowsComponents
helpviewer_keywords:
- Toolbox, Components tab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40ba84712a343a071d6213dc9cd985727fc20ebf
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560942"
---
# <a name="toolbox-components-tab"></a>ツールボックス、[コンポーネント] タブ

Visual Basic と C# の Windows フォーム デザイナーに追加できるコンポーネントを表示します。 <xref:System.Messaging.MessageQueue> コンポーネントや <xref:System.Diagnostics.EventLog> コンポーネントなど、Visual Studio に含まれている .NET コンポーネントに加え、独自のコンポーネントまたはサード パーティ製のコンポーネントをこのタブに追加できます。

このタブを表示するには、Windows フォーム デザイナーを開きます。 **[表示]** 、 **[ツールボックス]** の順に選択します。 **ツールボックス** で、**[コンポーネント]** タブを選択します。

## <a name="components"></a>コンポーネント

**BackgroundWorker**

別の専用スレッドで操作を実行できる <xref:System.ComponentModel.BackgroundWorker> コンポーネント インスタンスを作成します。 詳細については、「[BackgroundWorker コンポーネント](/dotnet/framework/winforms/controls/backgroundworker-component)」を参照してください。

**DirectoryEntry**

Active Directory 階層内のノードまたはオブジェクトをカプセル化し、Active Directory サービス プロバイダーとやり取りするために使用できる <xref:System.DirectoryServices.DirectoryEntry> コンポーネント インスタンスを作成します。

**DirectorySearcher**

Active Directory に対してクエリを実行するために使用できる <xref:System.DirectoryServices.DirectorySearcher> コンポーネント インスタンスを作成します。

**ErrorProvider**

エンド ユーザーにフォーム上のコントロールに関連付けられているエラーがあることを示す、<xref:System.Windows.Forms.ErrorProvider> コンポーネント インスタンスを作成します。 詳細については、「[ErrorProvider コンポーネント](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)」を参照してください。

**EventLog**

ログへのイベントの書き込みおよびログ データの読み込みなど、システムおよびカスタム イベント ログとやり取りするために使用できる <xref:System.Diagnostics.EventLog> コンポーネント インスタンスを作成します。

**FileSystemWatcher**

アクセス権がある任意のディレクトリまたはファイルへの変更を監視するために使用できる <xref:System.IO.FileSystemWatcher> コンポーネント インスタンスを作成します。

**HelpProvider**

コントロールのポップアップまたはオンライン ヘルプを提供する <xref:System.Windows.Forms.HelpProvider> コンポーネント インスタンスを作成します。 詳細については、「[HelpProvider コンポーネント](/dotnet/framework/winforms/controls/helpprovider-component-windows-forms)」を参照してください。

**ImageList**

<xref:System.Drawing.Image> オブジェクトのコレクションを管理するメソッドを提供する <xref:System.Windows.Forms.ImageList> コンポーネント インスタンスを作成します。 詳細については、「[ImageList コンポーネント](/dotnet/framework/winforms/controls/imagelist-component-windows-forms)」を参照してください。

**MessageQueue**

キューからメッセージを読み取る、メッセージをキューに書き込む、トランザクションの処理、およびキュー管理タスクの実行など、メッセージ キューとやり取りするために使用できる <xref:System.Messaging.MessageQueue> コンポーネント インスタンスを作成します。

**PerformanceCounter**

新しいカテゴリとインスタンスの作成、カウンターから値を読み取る、カウンター データに対して計算を実行するなど、Windows パフォーマンス カウンターとのやり取りに使用できる <xref:System.Diagnostics.PerformanceCounter> コンポーネント インスタンスを作成します。

**処理**

システム上のプロセスに関連付けられているデータを停止、開始、および操作できる <xref:System.Diagnostics.Process> コンポーネント インスタンスを作成します。

**SerialPort**

同期 I/O とイベント ドリブン I/O のフレームワーク、ピンの状態とブレーク状態へのアクセス、およびシリアル ドライバーのプロパティへのアクセスを提供する <xref:System.IO.Ports.SerialPort> コンポーネント インスタンスを作成します。

**ServiceController**

サービスの開始と停止やこれらのサービスへのコマンドの送信など、既存のサービスの操作に使用できる <xref:System.ServiceProcess.ServiceController> コンポーネント インスタンスを作成します。

**タイマー**

時間ベースの機能を Windows ベースのアプリケーションに追加するために使用できる <xref:System.Windows.Forms.Timer> コンポーネント インスタンスを作成します。 詳細については、「[Timer コンポーネント](/dotnet/framework/winforms/controls/timer-component-windows-forms)」を参照してください。

> [!NOTE]
> **ツールボックス** に追加できるシステム ベースの <xref:System.Timers.Timer> もあります。この <xref:System.Timers.Timer> は、サーバー アプリケーション用に最適化され、Windows フォーム <xref:System.Windows.Forms.Timer> は Windows フォームで使用するのに最も適しています。

## <a name="see-also"></a>関連項目

- [Windows フォームで使用するコントロール](/dotnet/framework/winforms/controls/controls-to-use-on-windows-forms)
- [ツールボックス アイテムの選択、WPF コンポーネント](choose-toolbox-items-wpf-components.md)
- [ツールボックス](../../ide/reference/toolbox.md)
