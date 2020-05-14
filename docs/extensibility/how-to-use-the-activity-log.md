---
title: '方法 : アクティビティ ログを使用する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 64986be303370cf8c9048612ff3d44e82e96805a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710578"
---
# <a name="how-to-use-the-activity-log"></a>方法: アクティビティ ログを使用する
VSPackage は、アクティビティ ログにメッセージを書き込むことができます。 この機能は、リテール環境で VSPackage をデバッグする場合に特に便利です。

> [!TIP]
> アクティビティ ログは常に有効です。 Visual Studio では、最後の 100 エントリのローリング バッファーと、一般的な構成情報を持つ最初の 10 個のエントリが保持されます。

## <a name="to-write-an-entry-to-the-activity-log"></a>アクティビティ ログにエントリを書き込むには

1. このコードを<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>メソッドまたは VSPackage コンストラクター以外の他のメソッドに挿入します。

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     このコードは、<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>サービスを取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>インターフェイスにキャストします。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A>現在のカルチャ コンテキストを使用して、アクティビティ ログに情報エントリを書き込みます。

2. VSPackage が読み込まれると (通常、コマンドが呼び出されるか、ウィンドウが開かれた場合)、テキストがアクティビティ ログに書き込まれます。

## <a name="to-examine-the-activity-log"></a>アクティビティ ログを調べるには

1. セッション中にディスクに ActivityLog.xml を書き込むには[、/Log](../ide/reference/log-devenv-exe.md)コマンド ライン スイッチを指定して Visual Studio を実行します。

2. Visual Studio を閉じた後、アクティビティ ログを Visual Studio データのサブフォルダーで探します。

   <em> *%アプリデータ%</em>\マイクロソフト\VisualStudio\\\<バージョン>\アクティビティログ.xml*.

3. 任意のテキスト エディタでアクティビティ ログを開きます。 典型的なエントリは次のとおりです。

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>信頼性の高いプログラミング

アクティビティ ログはサービスであるため、アクティビティ ログは VSPackage コンストラクターで使用できません。

アクティビティ ログは、書き込みの直前に取得する必要があります。 今後使用するためにアクティビティ ログをキャッシュまたは保存しないでください。

## <a name="see-also"></a>関連項目

- [/ログ (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
