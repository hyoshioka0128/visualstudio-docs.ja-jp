---
title: JIT の最適化とデバッグ | Microsoft Docs
description: 最適化されたコードは、されていないコードよりもデバッグが困難です。 JIT の最適化についてと、抑制するタイミングと方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 558a54f6ddcf4945da4937f75b8aa133949349a7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931085"
---
# <a name="jit-optimization-and-debugging"></a>JIT の最適化とデバッグ
コードをデバッグしようとする場合、コードが最適化されて **いない** 方が簡単です。 コードを最適化すると、コンパイラとランタイムにより、出力された CPU コードをより高速に実行できるように変更が行われますが、元のソース コードへのマッピングはあまり直接的ではありません。 マッピングがあまり直接的でないと、多くの場合に、デバッガーはローカル変数の値を示すことができず、コードのステップ実行やブレークポイントが期待どおりに機能しない可能性があります。

> [!NOTE]
> JIT (ジャストインタイム) デバッグの詳細については、[こちらのドキュメント](../debugger/debug-using-the-just-in-time-debugger.md)をお読みください。

## <a name="how-optimizations-work-in-net"></a>.NET での最適化のしくみ 
通常、リリース ビルド構成では最適化されたコードが作成されますが、デバッグ ビルド構成ではそれが作成されません。 `Optimize` MSBuild プロパティを使用して、コンパイラにコードを最適化するよう指示するかどうかを制御します。

.NET エコシステムでは、コードが 2 段階のプロセスでソースから CPU 命令に変換されます。最初に、入力したテキストが C# コンパイラによって MSIL という中間バイナリ形式に変換され、MSIL が .dll ファイルに書き込まれます。 その後、.NET ランタイムによって、この MSIL が CPU 命令に変換されます。 どちらのステップでもある程度最適化できますが、.NET ランタイムによって実行される 2 番目のステップでは、より大幅な最適化が行われます。

## <a name="the-suppress-jit-optimization-on-module-load-managed-only-option"></a>[モジュールの読み込み中に JIT 最適化を抑制する (マネージドのみ)] オプション
最適化を有効にしてコンパイルされた DLL がターゲット プロセス内で読み込まれたときの動作を制御するオプションがデバッガーによって公開されます。 このオプションがオフ (既定の状態) の場合、.NET ランタイムによって MSIL コードが CPU コードにコンパイルされると、最適化は有効なままになります。 このオプションをオンにすると、デバッガーによって最適化を無効にするように要求されます。

**[モジュールの読み込み時に JIT 最適化を抑制する (マネージのみ)]** オプションを見つけるには、 **[ツール]**  >  **[オプション]** を選択し、 **[デバッグ]** ノードの下にある **[全般]** ページを選択します。

![JIT 最適化の抑制](../debugger/media/suppress-jit-tool-options.png "JIT 最適化の抑制")

## <a name="when-should-you-check-the-suppress-jit-optimization-option"></a>[JIT 最適化を抑制する] オプションをオンにする必要があるケース
このオプションは、nuget パッケージなどの別のソースから DLL をダウンロードし、この DLL のコードをデバッグする場合にオンにします。 抑制を機能させるには、この DLL のシンボル (.pdb) ファイルも検索する必要があります。

このオプションを有効にすると、デバッグが大幅に遅くなる場合があるので、ローカルでビルドしているコードのデバッグにのみ関心がある場合は、このオプションをオフのままにすることをお勧めします。 この低速化には、次の 2 つの理由があります。

* 最適化されたコードの方が高速に実行されます。 多くのコードの最適化をオフにすると、パフォーマンスへの影響が大きくなる可能性があります。
* [マイ コードのみ] が有効になっている場合、デバッガーは最適化された DLL のシンボルの読み込みさえも試行しません。 シンボルの検索には長時間かかることがあります。

## <a name="limitations-of-the-suppress-jit-optimization-option"></a>[JIT 最適化を抑制する] オプションの制限 
このオプションをオンにすると機能 **しない** 状況が 2 つあります。

1. 既に実行中のプロセスにデバッガーをアタッチする場合、このオプションは、デバッガーがアタッチされた時点で既に読み込まれていたモジュールには影響しません。
2. このオプションは、ネイティブ コードに対してプリコンパイル済み (ngen 済み) の DLL には影響しません。 ただし、環境変数 **'COMPlus_ReadyToRun'** を **'0'** に設定してプロセスを開始することで、プリコンパイル済みコードの使用を無効にすることができます。 これにより、.NET Core ランタイムに、プリコンパイル済みイメージの使用を無効にし、ランタイムに JIT コンパイル フレームワーク コードを強制するように指示します。 

    > [!IMPORTANT]
    > .NET Framework または古いバージョンの .NET Core (2.x 以下) を対象としている場合は、環境変数 'COMPlus_ZapDisable' を追加し、それを '1' に設定します

    **Visual Studio 内で .NET Core プロジェクトの環境変数を設定するには:**
    1. **ソリューション エクスプローラー** で、プロジェクト ファイルを **右クリック** し、 **[プロパティ]** を選択します。
    2. **[デバッグ]** タブに移動し、 **[環境変数]** で **[追加]** ボタンをクリックします。
    3. 名前 (キー) を **COMPlus_ReadyToRun** に設定し、値を **0** に設定します。

    ![COMPlus_ReadyToRun 環境変数の設定](../debugger/media/environment-variables-debug-menu.png "COMPlus_ReadyToRun 環境変数の設定")

## <a name="see-also"></a>関連項目
- [方法: .Net Framework ソースをデバッグする](../debugger/how-to-debug-dotnet-framework-source.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [マネージド実行プロセス](/dotnet/standard/managed-execution-process)
