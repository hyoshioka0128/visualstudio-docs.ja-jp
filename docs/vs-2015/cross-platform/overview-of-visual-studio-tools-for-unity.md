---
title: Visual Studio Tools for Unity の概要 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: overview
ms.assetid: b4231bb9-45c4-4c77-ac3c-d05033b26393
caps.latest.revision: 6
ms.author: crdun
manager: crdun
ms.openlocfilehash: ba5447301c3a5581d35825ed91c17b3c9f50015f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298753"
---
# <a name="overview-of-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、Visual Studio Tools for Unity から提供される機能の概要と、Unity を使用する開発の生産性を向上させる方法について説明します。  
  
 Visual Studio tools Unity (*VSTU*) を利用すると、Visual Studio を使用して C# でゲームとエディター スクリプトを記述した後、強力なデバッガーを使用してエラーを検出して修正できます。 VSTU の最新リリースでは、Unity の ShaderLab シェーダー言語の構文の色分け、デバッガーの視覚化機能の向上、および、MonoBehavior ウィザードによるコード生成の機能強化などが行われました。 また、VSTU により、Unity のプロジェクト ファイル、コンソール メッセージ、およびゲームを開始する機能が Visual Studio に統合されるため、コードの記述中に Unity エディターとの間で切り替える手間を少なくできます。  
  
 これらの機能に関する詳細を、このあと説明します。  
  
## <a name="integration-with-unity"></a>Unity との統合  
 Unity エディターと Visual Studio を常に切り替えながら作業しなければならないとすると、Visual Studio Tools for Unity は生産性向上ツールであるとは言えません。 そのような理由から、Visual Studio Tools for Unity では、Visual Studio を離れずに簡単に作業できるようになっています。  
  
- **Unity プロジェクト エクスプローラー**を使用すると、Unity エディターに表示されるのと同じ階層構造で Visual Studio から Unity プロジェクト全体を見ることができます。  
  
- Unity コンソールとの統合により、Visual Studio のエラー ウィンドウに Unity コンソールからの出力が表示されます。  
  
- Visual Studio からゲームのデバッグを開始できます。Unity に切り替える必要はなく、F5 キーを押すだけです。  
  
## <a name="superior-debugging"></a>優れたデバッグ機能  
 スタンドアロンで実行されているか Unity エディターで実行されているかに関係なく、Visual Studio の強力なデバッガーを Unity ゲームに接続して、C# スクリプトと DLL をデバッグできます。 Visual Studio によって提供されるすべてのデバッグ機能を使用できます。  
  
- ブレークポイント (条件付きブレークポイントを含む)。  
  
- [ウォッチ] ウィンドウでの複雑な式の評価。  
  
- 変数および引数の値の検査と変更。  
  
- 複雑なオブジェクトやデータ構造体へのドリルダウン。  
  
  さらに、ネットワーク上の別のコンピューターで実行されている Unity ゲームであっても、デバッグできます。  
  
## <a name="productivity"></a>生産性  
 C# コードの記述とリファクタリングについての Visual Studio の確立された生産性に加えて、Visual Studio Tools for Unity は Unity 開発者のために追加の生産性機能を提供します。  
  
- Unity の ShaderLab 言語の構文が色分け表示されるため、バグになる前にシェーダーで間違いを見つけるために役立ちます。 これは、ShaderLab ファイルを Visual Studio で開くだけで機能します。  
  
- MonoBehavior ウィザードを使用すると、Unity の動作の一覧を参照し、使い慣れていない動作であっても、定型的なコードを作成できます。 Ctrl + Shift + M キーを押します。  
  
- よく使用する Unity の動作に慣れてきたら、クイック MonoBehavior ウィザードを使用して簡単に入力できます。 Ctrl + ALT + Q キーを押します。  
  
- Visual Studio から Unity のドキュメントにアクセスできます。 説明を読みたい API 呼び出しを強調表示し、Ctrl + ALT+M を押し、Ctrl + H を押します。  
  
- これらの機能すべてと、その他の機能は、キーボード ショートカットでアクセスできます。  
  
## <a name="visual-studio-tools-for-unity-api"></a>Visual Studio Tools for Unity の API  
 提供されている API を使用して、Visual Studio Tools for Unity の動作のカスタマイズや拡張を行えます。  
  
- Visual Studio Tools for Unity では、Unity コンソールを Visual Studio にストリーミングできるよう、Unity にログ コールバックを登録します。 情報を記録するエディター スクリプトがあれば、同じコールバックにそれらのスクリプトをプラグインして、Visual Studio にメッセージを送信できます。 詳細については、ログのコールバックの例を参照してください。  
  
- Visual Studio Tools for Unity がプロジェクト ファイルを生成する方法を変更するには、Unity のスタイル コールバック ProjectFileGeneration を使用します。 詳細については、プロジェクト ファイル生成の例を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Unity ホームページ](https://unity.com/)
