---
title: ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: eac59cb6-f12e-4a77-9953-6d62b164a643
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b3f38f519444de7876046baf242f74a18b8c5a59
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75844369"
---
# <a name="develop-apps-for-the-universal-windows-platform-uwp"></a>ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユニバーサル Windows プラットフォームと 1 つの Windows コアを使用することで、電話やデスクトップなどの Windows 10 デバイスで同じアプリを実行できます。 これらのユニバーサル Windows アプリは、Visual Studio 2015 とユニバーサル Windows アプリ開発ツールを使用して作成します。

 ![ユニバーサル Windows プラットフォーム](../cross-platform/media/uwp-coreextensions.png "UWP_CoreExtensions")

 アプリを Windows 10 Phone、Windows 10 デスクトップ、または Xbox で実行します。 同じアプリケーション パッケージが使用されています。 Windows 10 の単一の統一されたコアの導入により、1 つのアプリケーション パッケージをすべてのプラットフォームで実行できます。 いくつかのプラットフォームには、プラットフォーム固有の動作を利用するためにアプリに追加できる拡張 SDK があります。 たとえば、モバイル用の拡張 SDK を使用すれば、Windows Phone で [戻る] ボタンを処理できます。 プロジェクトで拡張 SDK を参照する場合、単純にランタイム チェックを追加して、プラットフォームでその SDK を使用できるかどうかをテストします。 このようにして、それぞれのプラットフォームで同じアプリケーション パッケージを使用できます。

 **Windows のコアとは何ですか。**

 Windows では初めて、すべての Windows 10 プラットフォームで共通のコアを持つようリファクタリングされました。 1 つの共有ソース、1 つの共通 Windows カーネル、1 つのファイル I/O スタック、および 1 つのアプリ モデルがあります。 UI については、1 つの XAML UI フレームワークと、1 つの HTML UI フレームワークしかありません。 さまざまな Windows 10 デバイス上でアプリを簡単に実行できるようになっているため、優れたアプリの作成に集中できます。

 **ユニバーサル Windows プラットフォームとは何ですか。**

 これはコントラクトとバージョンの単純なコレクションです。 これらにより、アプリを実行する対象となる場所を指定できます。 オペレーティング システムを対象とすることは、もはやありません。 今後は、1 つ以上のデバイス ファミリがアプリの対象になります。 詳しくは、この [プラットフォーム ガイド](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx)をご覧ください。

## <a name="requirements"></a>要件
 ユニバーサル Windows アプリの開発ツールには、別のデバイス上のアプリの外観を確認する際に使用できるエミュレーターが付属しています。 これらのエミュレーターを使用する場合は、このソフトウェアを物理マシンにインストールする必要があります。 その物理マシンでは、Windows 8.1 (x64) Professional エディション以上が実行され、クライアント Hyper-V および第 2 レベルのアドレス変換 (SLAT) をサポートするプロセッサが搭載されている必要があります。 Visual Studio が仮想マシンにインストールされている場合は、エミュレーターを使用できません。

 必要なソフトウェアの一覧を次に示します。

- [Windows 10](https://windows.microsoft.com/windows/downloads)

- [Visual Studio 2015](https://visualstudio.microsoft.com/downloads/)。 オプション機能の一覧からユニバーサル Windows アプリ開発ツールが選択されていることを確認します。 これらのツールがないと、ユニバーサル アプリを作成することができません。

  このソフトウェアをインストールしたら、開発用に [Windows 10 デバイスを有効にする](https://msdn.microsoft.com/library/windows/apps/xaml/dn706236.aspx) 必要があります。 (Windows 10 デバイスごとに開発者ライセンスは必要ありません。)

  **Windows 8.1 および Windows 7 のサポート**

  Windows 10 以外のプラットフォームで Visual Studio 2015 を使用してユニバーサル Windows アプリを開発する場合は、以下の制限事項があります。

- Windows 8.1: アプリをローカルで実行することはできません (リモート Windows 10 デバイスの場合のみ)。 Visual Studio でエミュレーターを使用できますが、シミュレーターを使用することはできません。

- Windows 7: アプリをローカルで実行することはできません (リモート Windows 10 デバイスの場合のみ)。 Visual Studio では、エミュレーターとシミュレーターのいずれも使用することはできません。

  開発プラットフォームが Windows 10 の場合に使用できるのは、XAML デザイナーのみです。

## <a name="universal-windows-apps"></a>ユニバーサル Windows アプリ
 希望する開発言語を C#、Visual Basic、C++ または JavaScript の中から選び、 [Windows 10 デバイスを対象とするユニバーサル Windows アプリを作成します](https://msdn.microsoft.com/library/windows/apps/xaml/dn609832.aspx#target_win10)。 あるいは [この入門用ビデオ](https://channel9.msdn.com/Series/ConnectOn-Demand/229)を再生します。

 既存の Windows 8.1 のストア アプリ、Windows Phone 8.1 アプリ、または Visual Studio 2015 RC で作成されたユニバーサル Windows アプリがある場合、最新のユニバーサル Windows プラットフォームを使用するよう、 [これらの既存のアプリを移植します](https://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) 。

 ユニバーサル Windows アプリを作成したら、 [アプリをパッケージ化して](https://msdn.microsoft.com/library/windows/apps/hh454036.aspx) 、それを Windows 10 デバイスにインストールするか Windows ストアに送信する必要があります。
