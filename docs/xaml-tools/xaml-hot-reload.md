---
title: XAML を使用した XAML の作成とデバッグホットリロード
description: XAML のホットリロード、または XAML のエディットコンティニュを使用すると、アプリの実行中に XAML コードを変更できます。
ms.date: 08/05/2019
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 120ae30b3a33a04f17bd2ec23b747ac41c9427cf
ms.sourcegitcommit: 5d1b2895d3a249c6bea30eb12b0ad7c0f0862d85
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "82921317"
---
# <a name="write-and-debug-running-xaml-code-with-xaml-hot-reload-in-visual-studio"></a>XAML を使用した実行中の XAML コードの作成とデバッグ Visual Studio でのホットリロード

XAML ホットリロードは、アプリの実行中に XAML コードを変更できるようにすることで、WPF または UWP アプリのユーザーインターフェイス (UI) を構築するのに役立ちます。 ホットリロードは、Visual Studio と Blend for Visual Studio の両方で使用できます。 この機能を使用すると、実行中のアプリのデータコンテキスト、認証状態、およびデザイン時にシミュレートするのが困難なその他の実際の複雑さの恩恵を受けながら、XAML コードを段階的にビルドおよびテストできます。 XAML ホットリロードのトラブルシューティングに関するヘルプが必要な場合は、「代わりに[Xaml ホットリロードのトラブルシューティング](xaml-hot-reload-troubleshooting.md)」を参照してください。

> [!NOTE]
> Xamarin. Forms を使用している場合は、「 [xamarin の XAML ホットリロード](/xamarin/xamarin-forms/xaml/hot-reload)」を参照してください。

XAML ホットリロードは、次のような場合に特に役立ちます。

* アプリがデバッグモードで起動された後に、XAML コードで見つかった UI の問題を修正します。

* アプリのランタイムコンテキストを活用しながら、開発中のアプリ用の新しい UI コンポーネントを構築します。

|サポートされているアプリケーションの種類|オペレーティング システムとツール|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 以降および .NET Core</br>Windows 7 以上 |
|ユニバーサル Windows アプリ (UWP)|Windows 10 以降、 [windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 + |

次の図は、ライブビジュアルツリーを使用してソースコードを開き、XAML ホットリロードを使用してボタンのテキストとボタンの色を変更する方法を示しています。

![XAML ホット リロード](../debugger/media/xaml-hot-reload-using.gif)

> [!NOTE]
> Visual Studio XAML ホットリロードは、現在、Visual Studio でアプリケーションを実行している場合、またはデバッガーがアタッチされた (**F5**または**デバッグを開始**する) Blend for Visual Studio 場合にのみサポートされます。 [環境変数を手動で設定](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)しない限り、[プロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)を使用してこのエクスペリエンスを有効にすることはできません。

## <a name="known-limitations"></a>既知の制限事項

XAML ホットリロードの既知の制限事項を次に示します。 に実行するすべての制限を回避するには、デバッガーを停止し、操作を完了します。

|制限事項|WPF|UWP|メモ|
|-|-|-|-|
|アプリの実行中にイベントをコントロールに接続する|サポートされていません|サポートされていません|「エラー:*イベントを確認できませんでした*」を参照してください。 WPF では、既存のイベントハンドラーを参照できます。 UWP アプリでは、既存のイベントハンドラーの参照はサポートされていません。|
|リソースディクショナリ内のリソースオブジェクト (アプリのページ/ウィンドウや*app.xaml*など) の作成|Visual Studio 2019 Update 2 以降でサポートされる|サポート状況|例: をと`SolidColorBrush`して使用するために、を`StaticResource`リソースディクショナリに追加します。</br>注: 静的リソース、スタイルコンバーター、およびリソースディクショナリに記述されたその他の要素は、XAML ホットリロードの使用中に適用または使用できます。 リソースの作成のみがサポートされていません。</br> リソースディクショナリ`Source`のプロパティを変更しています。|
|アプリの実行中に新しいコントロール、クラス、ウィンドウ、またはその他のファイルをプロジェクトに追加する|サポート非対象|サポート非対象|None|
|NuGet パッケージの管理 (パッケージの追加/削除/更新)|サポート非対象|サポート非対象|None|
|{X:Bind} markup extension を使用するデータバインディングの変更|N/A|Visual Studio 2019 以降でサポートされます。|これには、Windows 10 バージョン 1809 (build 10.0.17763) が必要です。 Visual Studio 2017 またはそれ以前のバージョンではサポートされていません。|
|X:Uid ディレクティブの変更はサポートされていません|なし|サポートしていません。|None|
|複数のプロセス | サポート非対象 | サポート非対象 | ホットリロードは、一度に1つのプロセスに対してのみ使用できます。 |

## <a name="error-messages"></a>エラー メッセージ

XAML ホットリロードの使用中に、次のエラーが発生する場合があります。

|エラー メッセージ|説明|
|-|-|
|イベントが失敗したことを確認する|[エラー] は、アプリケーションの実行中にサポートされていないコントロールの1つにイベントを送信しようとしていることを示します。|
|この変更は、XAML ホットリロードではサポートされておらず、デバッグセッション中に適用されません。|エラーは、実行しようとしている変更が XAML ホットリロードでサポートされていないことを示します。 デバッグセッションを停止し、変更を加えてから、デバッグセッションを再開します。 サポートが必要なサポートされていないシナリオが見つかった場合は、 [Visual Studio 開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/8/index.html)の新しい [機能の提案] オプションを使用してください。 |

## <a name="see-also"></a>関連項目

* [XAML ホット リロードのトラブルシューティング](xaml-hot-reload-troubleshooting.md)
* [Xamarin. フォームの XAML ホットリロード](/xamarin/xamarin-forms/xaml/hot-reload)
* [エディット コンティニュ (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
