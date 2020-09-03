---
title: Windows ストアアプリ用コンテンツのプリフェッチ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: b4481fef-3ebf-4f7d-9748-d43821a0ebac
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4ac6479b4dbb0815374174140deb0d660636ac9e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74300528"
---
# <a name="prefetch-content-for-windows-store-apps"></a>Windows ストア アプリ用コンテンツのプリフェッチ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows のみに適用されます] (../Image/windows_only_content.png "windows_only_content")  
  
 Windows ストアアプリの応答性を高めるために、web ページやイメージなどの一部の web コンテンツをアプリの [wininet](https://msdn.microsoft.com/0a06f2af-957a-4dff-a8cc-187370181b5c)[wininet](https://msdn.microsoft.com/library/aa383630.aspx)キャッシュにプリロードするように windows を要求することができます。 この機能をプリフェッチと呼びます。 これは起動時に使用されるコンテンツに特に効果的ですが、他の頻繁に使用するコンテンツをプリフェッチすることもできます。 [Windows.Networking.BackgroundTransfer.ContentPrefetcher](https://msdn.microsoft.com/library/windows/apps/windows.networking.backgroundtransfer.contentprefetcher.aspx) クラスのメソッドを使用すると、プリロードするコンテンツの URI を指定できます。  
  
 Windows は、プリフェッチを行う必要がある場合およびダウンロードするリソースを決定するためにヒューリスティックを使用します。 このヒューリスティックでは、システム ネットワークおよび電力条件、ユーザー アプリの使用履歴、および以前のプリフェッチの結果を考慮します。 Visual Studio では、**Trigger Windows Store App Prefetch** コマンドを使用することで、Windows に ContentPrefetcher ヒューリスティックを無視させ、さらに指定されたすべての Web コンテンツをプリロードさせることができます。 これは、既知の状態 (読み込まれている、または読み込まれていない) でプリフェッチするコンテンツでアプリの動作またはパフォーマンスをテストする場合に役立ちます。  
  
## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>ContentPrefetcher で指定されるリソースのプリロードを強制するには  
 この手順では、ContentPrefetcher 機能が既に設定されていて、アプリ プロジェクトでプリロードするコンテンツ URI が指定されていると仮定しています。 指定されたリソースが新しいまたは変更されている場合にコンテンツのプリロードを強制するには、**Trigger Windows Store App Prefetch** コマンドを選択する前にアプリを開始および停止する必要があります。 まず、アプリを実行して、URI を登録します。 **Trigger Windows Store App Prefetch** コマンドによって、ContentPrefetcher がコンテンツをダウンロードし、キャッシュに追加するように強制されます。 アプリの後続の実行で、コンテンツがプリロードされたと見なすことができます。  
  
1. アプリを開始して、アプリでプリフェッチ コンテンツ URI を登録します。 **[デバッグ]** メニューで、 **[デバッグの開始]** をクリックします (キーボード ショートカット: F5 キー)。  
  
2. **[デバッグ]** メニューの **[デバッグの停止]** をクリックします (キーボード ショートカット: Shift + F5)。  
  
3. **[デバッグ]** メニューで、 **[その他のデバッグ ターゲット]** をクリックし、 **[Windows ストア アプリ プリフェッチのトリガー]** をクリックします。  
  
   プリフェチした Web リソースでアプリをデバッグ、テスト、または分析できるようになりました。  
  
> [!NOTE]
> 指定された Web コンテンツを追加または変更するたびにこの手順を繰り返します。  
  
## <a name="see-also"></a>参照  
 [ブログの投稿:Visual Studio 2013 Update 2 で Windows ストア アプリ用のプリフェッチのトリガー](https://devblogs.microsoft.com/devops/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2/)
