---
title: UWP アプリでプリフェッチされたコンテンツを使用してデバッグする | Microsoft Docs
description: UWP アプリの応答性を高めるには、ContentPrefetcher を使用して、Web コンテンツのプリフェッチを Windows に要求します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- uwp
ms.openlocfilehash: 8f7cffe7f1e6edc482d4fec68908449c901d4ca2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891541"
---
# <a name="debug-uwp-apps-using-prefetched-content-in-visual-studio"></a>Visual Studio でプリフェッチされたコンテンツを使用して UWP アプリをデバッグする

 UWP アプリの応答性を高めるために、Web ページやイメージなどの一部の Web コンテンツをアプリの [WinINet](/windows/desktop/WinInet/about-wininet) キャッシュにプリロードするように Windows に要求できます。 この機能をプリフェッチと呼びます。 これは起動時に使用されるコンテンツに特に効果的ですが、他の頻繁に使用するコンテンツをプリフェッチすることもできます。 [Windows.Networking.BackgroundTransfer.ContentPrefetcher](/uwp/api/Windows.Networking.BackgroundTransfer.ContentPrefetcher) クラスのメソッドを使用すると、プリロードするコンテンツの URI を指定できます。 アプリに ContentPrefetcher 機能を追加する方法の例については、Windows SDK の「[Content prefetch sample](https://code.msdn.microsoft.com/windowsapps/ContentPrefetcher-Sample-432c8309)」 (コンテンツのプリフェッチの例) を参照してください。

 Windows は、プリフェッチを行う必要がある場合およびダウンロードするリソースを決定するためにヒューリスティックを使用します。 このヒューリスティックでは、システム ネットワークおよび電力条件、ユーザー アプリの使用履歴、および以前のプリフェッチの結果を考慮します。 Visual Studio では、**Trigger Windows Store App Prefetch** コマンドを使用することで、Windows に ContentPrefetcher ヒューリスティックを無視させ、さらに指定されたすべての Web コンテンツをプリロードさせることができます。 これは、既知の状態 (読み込まれている、または読み込まれていない) でプリフェッチするコンテンツでアプリの動作またはパフォーマンスをテストする場合に役立ちます。

## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>ContentPrefetcher で指定されるリソースのプリロードを強制するには
 この手順では、ContentPrefetcher 機能が既に設定されていて、アプリ プロジェクトでプリロードするコンテンツ URI が指定されていると仮定しています。 指定されたリソースが新しいまたは変更されている場合にコンテンツのプリロードを強制するには、**Trigger Windows Store App Prefetch** コマンドを選択する前にアプリを開始および停止する必要があります。 まず、アプリを実行して、URI を登録します。 **Trigger Windows Store App Prefetch** コマンドによって、ContentPrefetcher がコンテンツをダウンロードし、キャッシュに追加するように強制されます。 アプリの後続の実行で、コンテンツがプリロードされたと見なすことができます。

1. アプリを開始して、アプリでプリフェッチ コンテンツ URI を登録します。 **[デバッグ]** メニューで、 **[デバッグの開始]** をクリックします (キーボード ショートカット: F5 キー)。

2. **[デバッグ]** メニューの **[デバッグの停止]** をクリックします (キーボード ショートカット: Shift + F5)。

3. **[デバッグ]** メニューで、 **[その他のデバッグ ターゲット]** をクリックし、 **[Windows ストア アプリ プリフェッチのトリガー]** をクリックします。

   プリフェチした Web リソースでアプリをデバッグ、テスト、または分析できるようになりました。

> [!NOTE]
> 指定された Web コンテンツを追加または変更するたびにこの手順を繰り返します。

## <a name="see-also"></a>関連項目
- [ブログの投稿:Visual Studio 2013 Update 2 で Windows ストア アプリ用のプリフェッチのトリガー](https://devblogs.microsoft.com/devops/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2/)