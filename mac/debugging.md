---
title: Visual Studio for Mac を使用したデバッグ
description: デバッグは、プログラミングの中でも一般的で必要な部分です。 Visual Studio for Mac は成熟した IDE であり、デバッグが簡単になる機能一式が含まれています。 この記事では、安全なデバッグからデータの視覚化まで、Visual Studio for Mac のデバッグ機能を最大限に活用する方法について説明します。
author: therealjohn
ms.author: johmil
ms.date: 12/13/2019
ms.technology: vs-ide-debug
ms.assetid: BB7A084D-9AC2-48B5-8076-6C8518796BBA
ms.openlocfilehash: 8a12880c25e980d668351ef4c24ced1e479577d4
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "75397904"
---
# <a name="debugging-with-visual-studio-for-mac"></a>Visual Studio for Mac を使用したデバッグ

Visual Studio for Mac には、.Net Core、.NET Framework、Unity、および Xamarin アプリケーションをサポートするデバッガーが用意されています。

Visual Studio for Mac では、Visual Studio for Mac ですべてのプラットフォームでマネージド コードをデバッグするために、Mono ランタイムに実装されている [*Mono Soft Debugger*](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/) を使用しています。

## <a name="the-debugger"></a>デバッガー

Visual Studio for Mac では、すべての Xamarin アプリケーションのマネージド コード (C# または F#) をデバッグするために Mono Soft Debugger を使用しています。 Mono Soft Debugger は通常のデバッガーとは異なり、Mono ランタイムに組み込まれている協調的なデバッガーです。生成されたコードと Mono ランタイムが IDE と連携して、デバッグ エクスペリエンスが提供されます。 Mono ランタイムはワイヤ プロトコルを介してデバッグ機能を公開しています。詳細については、[Mono のドキュメント](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger-wire-format/)を参照してください。

[LLDB]( http://lldb.llvm.org/index.html) や [GDB]( https://www.gnu.org/software/gdb/) などのハード デバッガーの場合、デバッグ済みのプログラムの知識や連携を使用せずにプログラムを制御しますが、ネイティブ iOS または Android コードをデバッグする必要があり、Xamarin アプリケーションをデバッグするときには便利なことがあります。

.NET Core および ASP.NET Core アプリケーションの場合、Visual Studio for Mac では .NET Core デバッガーが使用されます。 このデバッガーは協調的なデバッガーでもあり、.NET ランタイムと連携して動作します。

## <a name="using-the-debugger"></a>デバッガーの使用

どのアプリケーションのデバッグを開始する場合でも、構成が **[デバッグ]** に設定されていることを確認します。 デバッグ構成は、ブレークポイントなどのデバッグ、データ ビジュアライザーの使用、コール スタックの表示をサポートする便利なツール セットです。

![デバッグ構成](media/debugging-image_0.png)

## <a name="setting-a-breakpoint"></a>ブレークポイントの設定

IDE でブレークポイントを設定するには、エディターで、中断するコードの行番号の横にある余白領域をクリックします。

![余白でのブレークポイントの設定](media/debugging-image0.png)

コードに設定したすべてのブレークポイントを表示するには、 **[ブレークポイント] パッド**を開きます。

![ブレークポイントの一覧](media/debugging-image0a.png)

## <a name="start-debugging"></a>デバッグを開始する

デバッグを開始するには、ターゲットのブラウザー、デバイス、またはミュレーター/エミュレーターを選択します。

![デバッグ構成](media/debugging-image_0.png)
![ターゲット デバイスの選択](media/debugging-image1.png)

**[再生]** ボタンを押すか、**Command キーを押しながら Return キー**を押してアプリケーションを展開します。 ブレークポイントにヒットすると、コードは黄色で強調表示されます。

![ブレークポイントにヒットしたことを示す強調表示](media/debugging-image2.png)

オブジェクト値の検査に使用できるツールなど、デバッグ ツールをこの時点で使用すると、コードで発生していることについて詳細情報を入手できます。

![デバッグの視覚化](media/debugging-image3.png)

## <a name="conditional-breakpoints"></a>条件付きブレークポイント

ブレークポイントが発生する状況を指示した規則を設定することもできます。これは*条件付きブレークポイント*の追加とも呼ばれます。 条件付きブレークポイントを設定するには、 **[ブレークポイントのプロパティ] ウィンドウ**にアクセスします。アクセスする方法は 2 つあります。

* 新しい条件付きブレークポイントを追加するには、ブレークポイントを設定するコードの行番号の左にあるエディターの余白を右クリックし、[ブレークポイントの作成] を選択します。

 ![ブレークポイント コンテキスト メニュー](media/debugging-image4.png)

* 既存のブレークポイントに条件を追加するには、ブレークポイントを右クリックし、 **[ブレークポイントのプロパティ]** を選択します。または **[ブレークポイント]** パッドで、次の図の [ブレークポイントの編集] ボタンを選択します。

 ![[ブレークポイント] パッドで既存のブレークポイントを編集する](media/debugging-image5.png)

この画面で、ブレークポイントが発生する条件を入力できます。

 ![ブレークポイント条件の編集](media/debugging-image6.png)

## <a name="stepping-through-code"></a>コードのステップ実行

デバッグ ツールでは、ブレークポイントに達すると、プログラムの実行を制御できます。 Visual Studio for Mac には、コードの実行とステップ実行に使用できるボタンが 4 つ表示されます。 Visual Studio for Mac では次のように表示されます。

 ![コードをステップ実行するボタン](media/debugging-image7.png)

この 4 つのボタンについて説明します。

* **再生** - コードの実行が開始され、次のブレークポイントまで実行されます。
* **ステップ オーバー** - 次のコード行が実行されます。 次行が関数呼び出しの場合、[ステップ オーバー] をクリックするとその関数が実行され、関数の*後*の次のコード行で停止します。
* **ステップ イン** - このボタンの場合も次のコード行が実行されます。 次行が関数呼び出しの場合、[ステップ イン] をクリックすると関数の最初の行で停止するので、関数のデバッグを 1 行ずつ続行できます。 次行が関数ではない場合の動作は、[ステップ オーバー] と同じです。
* **ステップ アウト** - 現在の関数が呼び出された行に戻ります。

## <a name="debugging-monos-class-libraries"></a>Mono のクラス ライブラリのデバッグ

Xamarin 製品には、Mono のクラス ライブラリのソース コードが付属しているため、デバッガーからのステップ実行にそのソース コードを利用して、内部でどのような処理が実行されているかを検査することができます。

この機能はデバッグ中に消費されるメモリが多いため、既定ではオフです。

この機能を有効にするには、 **[Visual Studio for Mac] > [ユーザー設定] > [デバッガー]** に移動し、次の図のように、" **[Step into external code]\(外部コードにステップ イン\)** " オプションが**オン**になっていることを確認します。

![外部コードにステップイン オプション](media/debugging-image8.png)

## <a name="see-also"></a>参照

- [Visual Studio でのデバッグ (Windows)](/visualstudio/debugger/)
