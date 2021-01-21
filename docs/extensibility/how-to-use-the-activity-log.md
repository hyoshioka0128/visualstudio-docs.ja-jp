---
title: '方法: アクティビティログを使用する |Microsoft Docs'
description: Vspackage は、アクティビティログにメッセージを書き込むことができます。 リテール環境で Vspackage をデバッグするためにアクティビティログを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2796b8537c0f94c02c91fddc73f6d913ba1b0c4c
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993576"
---
# <a name="how-to-use-the-activity-log"></a>方法: アクティビティログを使用する
Vspackage は、アクティビティログにメッセージを書き込むことができます。 この機能は、小売環境で Vspackage をデバッグする場合に特に便利です。

> [!TIP]
> アクティビティログは常にオンになっています。 Visual Studio では、最後の100エントリと、一般的な構成情報を持つ最初の10個のエントリのローリングバッファーが保持されます。

## <a name="to-write-an-entry-to-the-activity-log"></a>アクティビティログにエントリを書き込むには

1. このコード <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> は、VSPackage コンストラクターを除く、メソッドまたは他の任意のメソッドに挿入します。

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     このコードは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> サービスを取得し、それをインターフェイスにキャストし <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 現在のカルチャコンテキストを使用して、情報エントリをアクティビティログに書き込みます。

2. VSPackage が読み込まれると (通常はコマンドが呼び出されたとき、またはウィンドウが開かれたときに)、テキストがアクティビティログに書き込まれます。

## <a name="to-examine-the-activity-log"></a>アクティビティログを確認するには

1. [/Log](../ide/reference/log-devenv-exe.md)コマンドラインスイッチを使用して Visual Studio を実行し、セッション中にディスクに ActivityLog.xml を書き込みます。

2. Visual Studio を終了した後、Visual Studio データのサブフォルダーでアクティビティログを見つけます。

   <em> *% AppData%</em>\Microsoft\VisualStudio \\ \<version>\ActivityLog.xml*。

3. 任意のテキストエディターを使用して、アクティビティログを開きます。 一般的なエントリは次のとおりです。

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>信頼性の高いプログラミング

アクティビティログはサービスであるため、アクティビティログは VSPackage コンストラクターでは使用できません。

書き込みの直前にアクティビティログを取得する必要があります。 将来使用するために、アクティビティログをキャッシュまたは保存しないでください。

## <a name="see-also"></a>こちらもご覧ください

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
