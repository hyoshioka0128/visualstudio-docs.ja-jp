---
title: '方法: ARM デバイスでグラフィックス診断を使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 346fd3c0-9e92-4ab8-bb3b-1aa9000a2483
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5bbe12449849b656af2658c5bab667b0e611515e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685873"
---
# <a name="how-to-use-graphics-diagnostics-with-an-arm-device"></a>方法: ARM デバイスでグラフィックス診断を使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス診断は、Windows RT 8.1 または Windows Phone 8.1 を実行する ARM ベースのデバイスで Direct3D アプリケーションのリモート デバッグをサポートします。 Direct3D がデバイス上で実行されている間に、Direct3D アプリケーショングラフィックス情報をキャプチャできます。また以前にキャプチャしたグラフィックス情報については、デバイスを再生コンピューターとして使用できます。  
  
## <a name="using-graphics-diagnostics-with-an-arm-based-device"></a>ARM ベースのデバイスでのグラフィックス診断の使用  
 Visual Studio は ARM ベースのデバイス上では稼動しないため、これらのデバイス上で稼動するアプリケーションを分析するにはリモート デバッガーを使用する必要があります。 リモート デバッガーはグラフィックスのキャプチャと再生をサポートしているため、アプリケーションをデバッグするのと同じくらい簡単に、レンダリングのエラーを診断し、これらのデバイスのグラフィックス パフォーマンスを評価することができます。  
  
 グラフィックス診断の機能を使用するには、最初にデバイス上でリモート デバッギングを有効にします。  
  
#### <a name="to-enable-remote-debugging-on-your-arm-based-device"></a>ARM ベースのデバイス上でリモート デバッギングを有効にするには  
  
1. Arm ベースのデバイスに [Arm キットポリシー](https://msdn.microsoft.com/windows/desktop/dn469188) をインストールします。  
  
2. ARM ベースのデバイスに [リモートデバッグツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015) をインストールします。  
  
> [!IMPORTANT]
> Windows Phone 8.1 のデバイスの場合は、開発用にスマートフォンを登録しなければならないことがあります。 そのためには、自身が登録されている開発者であることが必要です。 詳細については、「 [Windows Phone 8 用にアプリをデプロイして実行する方法](https://msdn.microsoft.com/library/windowsphone/develop/ff402565.aspx)」を参照してください。  
  
 デバイス上でリモート デバッギングを有効にしたら、デバイスをデバッグ ターゲットにしてグラフィックス診断を開始します。  
  
#### <a name="to-configure-and-start-graphics-diagnostics-on-your-device"></a>デバイス上でグラフィックス診断を構成および開始するには  
  
1. ARM ベースのデバイスをリモートデバッグターゲットとして使用できるようにするには、[ **ソリューションプラットフォーム** ] ドロップダウンリストで [ **arm** ] を選択します。  
  
2. [ **デバッグターゲット** ] ドロップダウンリストで、ARM デバイスを選択します。  
  
3. メニューで、[ **デバッグ**]、[ **グラフィックス**]、[ **診断の開始**] の順に選択します。 (キーボード: Alt + F5)  
  
## <a name="see-also"></a>参照  
 [リモートコンピューターでの Windows ストアアプリの実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)   
 [方法: グラフィックス診断再生マシンを変更する](../debugger/how-to-change-the-graphics-diagnostics-playback-machine.md)
