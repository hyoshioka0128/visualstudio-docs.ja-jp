---
title: JIT の最適化とデバッグ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], optimized code
- optimized code, debugging
ms.assetid: 19bfabf3-1a2e-49dc-8819-a813982e86fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae11860aaa64448cd4d23b5602cf4c2da1575ce3
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916217"
---
# <a name="jit-optimization-and-debugging"></a>JIT の最適化とデバッグ
コードをデバッグする場合は、そのコードが最適化されて**いない**と簡単になります。 コードを最適化すると、コンパイラとランタイムは、出力された CPU コードをより高速に実行できるように変更を行いますが、元のソースコードへの直接マッピングはあまりありません。 マッピングがあまり直接的でない場合、多くの場合、デバッガーはローカル変数の値を示すことができず、コードのステップ実行やブレークポイントが期待どおりに機能しない可能性があります。

> [!NOTE]
> JIT (ジャストインタイム) デバッグの詳細については、こちらの[ドキュメント](../debugger/debug-using-the-just-in-time-debugger.md)を参照してください。

## <a name="how-optimizations-work-in-net"></a>.NET での最適化のしくみ 
通常、リリースビルド構成によって最適化されたコードが作成され、デバッグビルド構成は作成されません。 `Optimize` MSBuild プロパティは、コードを最適化するようにコンパイラに指示するかどうかを制御します。

.NET エコシステムでは、コードが2段階のプロセスでソースから CPU への命令に変換されC#ます。最初に、コンパイラは、入力したテキストを msil という中間バイナリ形式に変換し、msil を .dll ファイルに書き込みます。 その後、.NET ランタイムは、この MSIL を CPU 命令に変換します。 どちらの手順でも程度を最適化できますが、.NET ランタイムによって実行される2番目のステップでは、より重要な最適化が実行されます。

## <a name="the-suppress-jit-optimization-on-module-load-managed-only-option"></a>[モジュールの読み込み時に JIT 最適化を抑制する (マネージのみ)] オプション
デバッガーは、最適化を有効にしてコンパイルされた DLL がターゲットプロセス内で読み込まれたときの動作を制御するオプションを公開します。 このオプションがオフの場合 (既定の状態)、.NET ランタイムが MSIL コードを CPU コードにコンパイルすると、最適化が有効になります。 このオプションをオンにすると、デバッガーは最適化を無効にするように要求します。

**[モジュールの読み込み時に JIT 最適化を抑制する (マネージのみ)]** オプションを見つけるには、[**ツール** > **オプション**] を選択し、 **[デバッグ]** ノードの下の **[全般]** ページを選択します。

![JIT 最適化の抑制](../debugger/media/suppress-jit-tool-options.png "JIT 最適化の抑制")

## <a name="when-should-you-check-the-suppress-jit-optimization-option"></a>[JIT 最適化を抑制する] オプションをオンにする場合は、
このオプションは、nuget パッケージなどの別のソースから Dll をダウンロードし、この DLL のコードをデバッグする場合にオンにします。 抑制を機能させるには、この DLL のシンボル (.pdb) ファイルも検索する必要があります。

ローカルでビルドしているコードのデバッグにのみ関心がある場合は、このオプションをオフのままにすることをお勧めします。このオプションを有効にすると、デバッグが大幅に遅くなる場合があります。 この速度が低下する理由は2つあります。

* 最適化されたコードの実行速度が向上します。 多くのコードの最適化を無効にすると、パフォーマンスへの影響が大きくなる可能性があります。
* マイコードのみ有効になっている場合、デバッガーは最適化された Dll のシンボルの読み込みを試行しません。 シンボルの検索には長い時間がかかることがあります。

## <a name="limitations-of-the-suppress-jit-optimization-option"></a>[JIT 最適化を抑制する] オプションの制限事項 
このオプションをオンにすると、次の2つの**状況が発生**します。

1. 既に実行中のプロセスにデバッガーをアタッチする場合、このオプションは、デバッガーがアタッチされた時点で既に読み込まれていたモジュールには影響しません。
2. このオプションは、ネイティブコードに対してプリコンパイル済み (. k. a...) の Dll には影響しません。 ただし、環境変数 **' COMPlus_ReadyToRun '** を **' 0 '** に設定してプロセスを開始することで、プリコンパイル済みコードの使用を無効にすることができます。 これにより、.NET Core ランタイムは、プリコンパイル済みイメージの使用を無効にし、ランタイムに JIT コンパイルフレームワークコードを強制するように指示します。 

    > [!IMPORTANT]
    > .NET Framework または古いバージョンの .NET Core (2.x 以下) を対象としている場合は、環境変数 ' COMPlus_ZapDisable ' を追加し、それを ' 1 ' に設定します。

    **Visual Studio で .NET Core プロジェクトの環境変数を設定するには、次のようにします。**
    1. **ソリューションエクスプローラー**で、プロジェクトファイルを**右クリック**し、 **[プロパティ]** を選択します。
    2. **[デバッグ]** タブに移動し、 **[環境変数]** で **[追加]** ボタンをクリックします。
    3. [名前 (キー)] を**COMPlus_ReadyToRun**に設定し、値を**0**に設定します。

    ![環境変数の設定 COMPlus_ReadyToRun](../debugger/media/environment-variables-debug-menu.png "環境変数の設定 COMPlus_ReadyToRun")

## <a name="see-also"></a>関連項目
- [Dotnet Framework ソースをデバッグする方法](../debugger/how-to-debug-dotnet-framework-source.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [マネージド実行プロセス](/dotnet/standard/managed-execution-process)
