---
title: '方法: 特定のリリースをインストールする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- install a specific release, Visual Studio
ms.assetid: d69ad0f8-f0a0-438e-a0ef-777c4868f139
caps.latest.revision: 20
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: dde0cefabf0523484ad76ac56f7f2760de8c7acc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433073"
---
# <a name="how-to-install-a-specific-release-of-visual-studio"></a>方法: Visual Studio の特定のリリースをインストールする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

最新で最適化されたバージョンのオプション機能をご利用いただけるよう、Visual Studio のセットアップは頻繁に更新されています。  しかし、以前のリリースの Visual Studio 2015 (たとえば、iOS サポートが含まれている Update 1 より前のリリースの Visual Studio 2015) をインストールする場合は、Visual Studio セットアップで強制的に以前のバージョンのフィーチャー マニフェスト ファイルを使用する必要があります。 この記事では、その方法について説明します。

## <a name="installing-the-current-release"></a>現在のリリースのインストール
 Visual Studio 2015 の最初のリリース以来、セットアップ エンジンとマニフェスト ファイルは何度か更新されています。  つまり、[Visual Studio のダウンロード](https://www.visualstudio.com/downloads/download-visual-studio-vs) Web サイトから、インターネットに接続されたクリーンなコンピューター上に Web インストーラーをダウンロードした場合、セットアップによって Visual Studio 2015 の最新の更新プログラムがインストールされます。これには、製品の最新の機能強化と、最近のより新しいバージョンのオプション機能やツールが含まれます。

## <a name="installing-earlier-releases"></a>以前のリリースのインストール
 Visual Studio のインストール方法を制御するには、ISO イメージを作成してマウントすることも、[My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) から直接インストーラーをダウンロードして実行してから、追加のコマンド ライン パラメーター (/CustomInstallPath、/Full、/InstallSelectableItems、/NoRestart など) によって .exe ファイルを追加することもできます。

 特定の時点でのシナリオと、Enterprise エディションのインストーラーに渡す必要のあるコマンド ライン パラメーターを、次の表にいくつか示します。 (同じパラメーターは、Community または Professional エディションのインストーラーでも機能します)。

|Visual Studio 2015 エディション|実行対象|使用するコマンド ライン|セットアップの機能|
|--------------------------------|-----------------|--------------------------|---------------------|
|Visual Studio Enterprise (最新の公開リリース)|Visual Studio Enterprise with Updates ([My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) から入手可能)|`vs_enterprise.exe` **注:** このインストールの既定の動作では、最新のオプション機能が提供されるため、コマンド ライン パラメーターは必要ありません。|Visual Studio セットアップでは、最新の feed.xml が使われ、最新のファイルがインストールされます|
|Visual Studio Enterprise Update 3 (Update 3 になってからの更新プログラムを何も含んでいない、オリジナルの Update 3)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160628.2/enu/feed.xml`|Visual Studio セットアップでは、Update 3 のリリース時に利用可能だった feed.xml が使われます|
|Visual Studio Enterprise Update 2 (オリジナルの Update 2 ですが、Update 3 より前の更新プログラムが含まれます)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160620.2/enu/feed.xml`|Visual Studio セットアップでは、Update 3 がリリースされるまで最新だった feed.xml を使用します|
|Visual Studio Enterprise (Update 2 になってからの更新プログラムを含まない、オリジナルの Update 2)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/0/6/B/06BB0C5C-C767-4250-91DA-AB463377597E/20160405.3/enu/feed.xml`|Visual Studio セットアップでは、Update 2 のリリース時に利用可能だった feed.xml が使われます|
|Visual Studio Enterprise Update 1 (オリジナルの Update 1 ですが、Update 2 より前の更新プログラムが含まれます)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20160225.3/enu/feed.xml`|Visual Studio セットアップでは、Update 2 がリリースされるまで最新だった feed.xml を使用します|
|Visual Studio Enterprise Update 1 (Update 1 になってからの更新プログラムを何も含んでいない、オリジナルの Update 1)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20151201.1/enu/feed.xml`|Visual Studio セットアップでは、Update 1 のリリース時に利用可能だった feed.xml が使われます|
|Visual Studio Enterprise (オリジナルの RTM ではあるものの、Update 1 より前の更新プログラムを持つもの)|Visual Studio Enterprise RTM (  [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/6/1/36188D5F-479F-4A46-BF55-6AE5928D1EBB/20151102.3/enu/feed.xml`|Visual Studio セットアップでは、Update 1 がリリースされるまで最新だった feed.xml を使用します。|
|Visual Studio Enterprise (更新プログラムのないオリジナルの RTM)|Visual Studio Enterprise RTM ( [MSDN サブスクリプションのダウンロード ページ](https://msdn.microsoft.com/subscriptions/downloads/)から入手可能)|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/5/7/B/57BF5016-E4F0-4EB5-BE27-2BFA87E7723F/20150713.1/enu/feed.xml`|Visual Studio セットアップでは、RTM のリリース時に利用可能だった feed.xml が使われます|

> [!IMPORTANT]
> 使用する言語によって、"enu" (英語) を次の値のいずれかに置き換えてください。
>
> - chs (簡体中国語)
>   - cht (繁体中国語)
>   - csy (チェコ語)
>   - deu (ドイツ語)
>   - esn (スペイン語)
>   - fra (フランス語)
>   - ita (イタリア語)
>   - jpa (日本語)
>   - kor (韓国語)
>   - plk (ポーランド語)
>   - ptb (ポルトガル語)
>   - rus (ロシア語)
>   - trk (トルコ語)

## <a name="see-also"></a>関連項目
 [Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)
