---
title: Visual Studio と Xamarin | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: 1da4064f-af69-472c-8f31-98484be5f790
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 098d94a1aed9020271db5010e278a4aa8fc68330
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842189"
---
# <a name="visual-studio-and-xamarin"></a>Visual Studio と Xamarin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Xamarin はネイティブの iOS、Android、および Windows のアプリを一般的な C#/.NET コード ベースから構築するためのモバイル アプリ開発プラットフォームであり、プラットフォーム間で 75% ～ほぼ 100% のコードの再利用を達成しています。 Xamarin と C# で記述されたアプリは、基礎となるプラットフォーム API にフル アクセスでき、ネイティブ ユーザー インターフェイスを構築する機能を装備しています。プラットフォーム固有のパッケージにコンパイルするので、実行時のパフォーマンスにほとんど影響を与えることがありません。 (注: Xamarin は F# もサポートしていますが、このドキュメントでは C# のみを扱います。 Visual Basic は現時点ではサポートされていません。)  
  
 さらに良いことに、C#、.NET、および Visual Studio に慣れている開発者は、Android、iOS、および Windows デバイスでのリモート デバッグなど、モバイル アプリを Xamarin で開発する場合、Objective-C または Java のようなネイティブのコーディング言語を習得しなくても、同じ機能と生産性を享受できます。 これは驚くことではありません。NASCAR、Aviva や MixRadio のような、素晴らしい ユーザー インターフェイスを持つ高性能なアプリの多くは、Xamarin を使用して作成されているからです。  
  
 このドキュメントでは、以下の項目を通して **Xamarin を使用した Visual Studio** のすべての機能を評価することができます。  
  
- 最初に、時間のかかるプロセスである[セットアップとインストール](../cross-platform/setup-and-install.md)を行います (インターネット接続の速度、既にインストールしているものや選択するオプションによって異なりますが、通常 2 ～ 4 時間)。  
  
- インストーラーが実行している間、「[Xamarin によるモバイル開発の概要](../cross-platform/learn-about-mobile-development-with-xamarin.md)」を確認し、Xamarin の性質や Xamarin.Forms とネイティブ UI との比較などを理解しましょう。  
  
- インストールが完了したら、[Xamarin 環境を検証する](../cross-platform/verify-your-xamarin-environment.md)作業を実行します。  
  
- チュートリアル「[Visual Studio での Xamarin Froms を使用したアプリ作成の基本事項](../cross-platform/learn-app-building-basics-with-xamarin-forms-in-visual-studio.md)」を確認して、作業を仕上げます。  
  
  [任意のエディションの Visual Studio 2015](https://www.visualstudio.com/vs-2015-product-editions) (Community、Professional、および Enterprise) で、Xamarin のすべての機能を使用することができます。 2016 年 3 月 31日の時点で、Xamarin はすべてのエディションの Visual Studio 2015 に含まれており、個別のライセンスは不要になりました。 Visual Studio 2013 については、「[セットアップとインストール](../cross-platform/setup-and-install.md)」で説明されているように、Xamarin を個別にインストールすることができます。  
  
> [!NOTE]
> これらの手順では、Windows および Visual Studio を背景とした場合の最も簡単で単純なコンピューターの構成について説明します。 この構成を使用すると、Mac と対話するだけで iOS シミュレーターとテザリングされたデバイスを使用できるので、開発作業全体が簡略化されます。 Mac に慣れている場合には、Parallels/VMWare 内の Visual Studio を実行するか、Xamarin Studio Community を使用することをお勧めします。 詳細については、「[Setup, install, and verifications for Mac users](../cross-platform/setup-install-and-verifications-for-mac-users.md)」(Mac ユーザー向けのセットアップ、インストール、および 検証) をご覧ください。  
  
> [!NOTE]
> HTML と CSS に基づくクロスプラットフォーム開発ソリューションを探している場合は、「 [Visual Studio でのクロスプラットフォーム開発](../cross-platform/cross-platform-mobile-development-in-visual-studio.md#HTML)」で説明されているように、Apache Cordova の Visual Studio Tools を確認してください。
