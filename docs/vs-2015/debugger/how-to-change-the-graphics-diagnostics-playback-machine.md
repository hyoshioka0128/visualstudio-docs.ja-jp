---
title: '方法: グラフィックス診断再生マシンを変更する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1b9aa3ea-29a0-4e21-bc57-936f33537b5c
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb14fb4017ea1df6659b9a1a0ac093cd7cf7e0b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841873"
---
# <a name="how-to-change-the-graphics-diagnostics-playback-machine"></a>方法: グラフィックス診断再生マシンを変更する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカル コンピューターを使用するか、リモート コンピューターまたはリモート デバイスを使用して、グラフィックス情報を再生できます。  
  
## <a name="choosing-a-playback-machine"></a>再生コンピューターの選択  
 再生コンピューターは、グラフィックス ログからグラフィックス イベントを再生するために使用されるコンピューターまたはデバイスです。 通常はローカル コンピューターが最も便利ですが、レンダリングの問題は、問題がキャプチャされたコンピューターとはハードウェアやドライバーのバージョンが異なるコンピューターで再現しない場合があります。その場合は、問題を適切に再現するリモート再生コンピューターを選択し、開発用コンピューターを使用して診断することができます。  
  
#### <a name="to-use-the-local-machine-to-play-back-graphics-information"></a>ローカル コンピューターを使用してグラフィックス情報を再生するには  
  
1. グラフィックス ログのドキュメント ウィンドウで、 **[再生コンピューター]** リンクをクリックします。 **[リモート デバッガー接続]** ダイアログ ボックスが表示されます。  
  
2. **[手動で構成]** の下の **[アドレス]** プロパティに、「`localhost`」と入力します。  
  
3. **[認証モード]** プロパティを **[なし]** に設定します。  
  
4. **[選択]** ボタンを選択します。  
  
#### <a name="to-use-a-remote-machine-to-play-back-graphics-information"></a>リモート コンピューターを使用してグラフィックス情報を再生するには  
  
1. グラフィックス ログのドキュメント ウィンドウで、 **[再生コンピューター]** リンクをクリックします。 **[リモート デバッガー接続]** ダイアログ ボックスが表示されます。  
  
2. **[手動で構成]** の下の **[アドレス]** プロパティにグラフィックス情報を再生するために使用するコンピューターまたはデバイスの Windows ドメイン名または IP アドレスを入力します。  
  
3. 再生コンピューターへの接続を保護するために使用する承認の種類を指定します。  
  
    - Windows 認証の場合は、 **[認証モード]** プロパティを **[Windows]** に設定します。  
  
    - 認証を使用しない場合は、 **[認証モード]** プロパティを **[なし]** に設定します。  
  
4. **[選択]** ボタンを選択します。  
  
> [!NOTE]
> **[リモート デバッガー接続]** ダイアログ ボックスには、開発用コンピューターに直接接続されているか、同じサブネット上にある、リモート デバッグ ターゲットも表示されることがあります。 これらのリモート デバッグ ターゲットのいずれかを、手動で構成せずに、グラフィックス診断再生コンピューターとして使用できます。 **[リモート デバッガー接続]** ダイアログ ボックスで、目的のターゲットを選択し、 **[選択]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [グラフィックス ログ ドキュメント](../debugger/graphics-log-document.md)
