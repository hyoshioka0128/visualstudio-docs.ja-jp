---
title: ツールボックス、[コンポーネント] タブ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Toolbox, Components tab
ms.assetid: 332fafab-a763-4244-b388-15d1b5b5cc04
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ce18767d95b3ac539737d78acbd2259dcda0a036
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72661564"
---
# <a name="toolbox-components-tab"></a>ツールボックス、[コンポーネント] タブ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] および [!INCLUDE[csprcs](../../includes/csprcs-md.md)] のデザイナーに追加できるコンポーネントを表示します。 コンポーネント [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] やコンポーネントなど、に付属するコンポーネントに加えて、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 独自の <xref:System.Messaging.MessageQueue> <xref:System.Diagnostics.EventLog> コンポーネントまたはサードパーティのコンポーネントをこのタブに追加できます。詳細については、「 [方法: ツールボックスタブを操作する](https://msdn.microsoft.com/21285050-cadd-455a-b1f5-a2289a89c4db)」を参照してください。

 このタブを表示するには、[**表示**] メニューで [**ツールボックス**] を選択します。 **ツールボックス**で、[**コンポーネント**] タブをクリックします。

 **BackgroundWorker**`System.ComponentModel.BackgroundWorker`個別の専用スレッドで操作を実行できるコンポーネントインスタンスを作成します。

 **DirectoryEntry**<xref:System.DirectoryServices.DirectoryEntry>Active Directory 階層内のノードまたはオブジェクトをカプセル化し、Active Directory サービスプロバイダーとの対話に使用できるコンポーネントインスタンスを作成します。

 **DirectorySearcher** Active Directory に <xref:System.DirectoryServices.DirectorySearcher> 対してクエリを実行するために使用できるコンポーネントインスタンスを作成します。

 **ErrorProvider**`System.Windows.Forms.ErrorProvider`フォーム上のコントロールにエラーが関連付けられていることをエンドユーザーに示すコンポーネントインスタンスを作成します。

 **イベントログ**<xref:System.Diagnostics.EventLog>ログへのイベントの書き込みやログデータの読み取りなど、システムおよびカスタムイベントログとの対話に使用できるコンポーネントインスタンスを作成します。 詳細については、「[Introduction to the EventLog Component](https://msdn.microsoft.com/a2ba4f28-4b1a-435e-99ef-51b28e21f805)」 (EventLog コンポーネントの概要) を参照してください。

 **FileSystemWatcher** アクセス権 <xref:System.IO.FileSystemWatcher> のあるディレクトリまたはファイルへの変更を監視するために使用できるコンポーネントインスタンスを作成します。 詳細については、「[How to: Configure FileSystemWatcher Component Instances](https://msdn.microsoft.com/2e628234-4951-4135-8a86-28b924070d50)」 (方法: FileSystemWatcher コンポーネント インスタンスの構成) を参照してください。

 **HelpProvider**`System.Windows.Forms.HelpProvider`コントロールのポップアップまたはオンラインヘルプを提供するコンポーネントインスタンスを作成します。

 **ImageList**`System.Windows.Forms.ImageList`オブジェクトのコレクションを管理するメソッドを提供するコンポーネントインスタンスを作成し `System.Drawing.Image` ます。

 **MessageQueue** メッセージ <xref:System.Messaging.MessageQueue> キューとのやり取りに使用できるコンポーネントインスタンスを作成します。これには、キューからのメッセージの読み取り、キューへのメッセージの書き込み、トランザクションの処理、およびキュー管理タスクの実行が含まれます。 詳細については、「[Using Messaging Components](https://msdn.microsoft.com/922dbac7-26f0-4e39-b666-ccfc184793d7)」 (メッセージング コンポーネントの使用) を参照してください。

 **PerformanceCounter**<xref:System.Diagnostics.PerformanceCounter>新しいカテゴリとインスタンスの作成、カウンターからの値の読み取り、カウンターデータに対する計算の実行など、Windows パフォーマンスカウンターとの対話に使用できるコンポーネントインスタンスを作成します。 詳細については、「[Monitoring Performance Thresholds](https://msdn.microsoft.com/b8b44a55-31d0-4b45-9517-8c1b1e4fdc91)」(パフォーマンスのしきい値の監視) をご覧ください。

 **プロセス**<xref:System.Diagnostics.Process>システム上のプロセスに関連付けられたデータを停止、開始、および操作するために使用できるコンポーネントインスタンスを作成します。 詳細については、「[Monitoring and Managing Windows Processes](https://msdn.microsoft.com/a86bd4c1-b92c-49a0-8f32-61d67837b45e)」 (Windows プロセスの監視と管理) を参照してください。

 **SerialPort**`System.IO.Ports.SerialPort`同期およびイベントドリブン i/o、ピンとブレークの状態へのアクセス、およびシリアルドライバーのプロパティへのアクセスを提供するコンポーネントインスタンスを作成します。

 **ServiceController** サービスの <xref:System.ServiceProcess.ServiceController> 開始と停止、それらへのコマンドの送信など、既存のサービスを操作するために使用できるコンポーネントインスタンスを作成します。 詳細については、「[Monitoring Windows Services](https://msdn.microsoft.com/4542ee3f-e052-4cb9-8726-58e9420de222)」 (Windows サービスの監視) を参照してください。

 **タイマー**<xref:System.Windows.Forms.Timer>Windows ベースのアプリケーションに時間ベースの機能を追加するために使用できるコンポーネントインスタンスを作成します。 詳細については、「[Timer コンポーネント](https://msdn.microsoft.com/library/6700e534-6382-43d5-98ed-14205435fff7)」を参照してください。

> [!NOTE]
> **ツールボックス**に追加できるシステム ベースの <xref:System.Timers.Timer> もあります。この <xref:System.Timers.Timer> は、サーバー アプリケーション用に最適化され、Windows フォーム <xref:System.Windows.Forms.Timer> は Windows フォームで使用するのに最も適しています。

## <a name="see-also"></a>参照
 [コンポーネントを使用したプログラミングコンポーネントの](https://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3)[プログラミングチュートリアル](https://msdn.microsoft.com/library/373cacf7-479e-4b05-991c-5cb18824e913)[ツール](../../ide/reference/toolbox.md)ボックスの[[ツールボックスアイテムの選択] ダイアログボックス (Visual Studio)](https://msdn.microsoft.com/bd07835f-18a8-433e-bccc-7141f65263bb)
