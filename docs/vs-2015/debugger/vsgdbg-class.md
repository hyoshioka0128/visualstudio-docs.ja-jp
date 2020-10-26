---
title: VsgDbg クラス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 6722263c-ccef-40c7-a0ae-87a863fbab00
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 053647d48324f056148375bae9268b997ba8721f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145689"
---
# <a name="vsgdbg-class"></a>VsgDbg クラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス診断のアプリ内コンポーネントのプログラムによる制御のインターフェイスを表します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
class VsgDbg;  
```  
  
## <a name="members"></a>メンバー  
 `VsgDbg` クラスは、次のメンバーをサポートします。  
  
### <a name="public-constructors"></a>パブリック コンストラクター  
  
|名前|説明|  
|----------|-----------------|  
|[VsgDbg::VsgDbg (コンストラクター)](../debugger/vsgdbg-vsgdbg-constructor.md)|`VsgDbg` クラスのインスタンスを構築し、オプションで、グラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備します。|  
|[VsgDbg::~VsgDbg (デストラクター)](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)|`VsgDbg` クラスのインスタンスを破棄します。|  
  
### <a name="public-methods"></a>パブリック メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[AddMessage](../debugger/addmessage.md)|グラフィックス診断の HUD (ヘッドアップ ディスプレイ) にカスタム メッセージを追加します。|  
|[BeginCapture](../debugger/begincapture.md)|`EndCapture` で終了するキャプチャ区間を開始します。|  
|[CaptureCurrentFrame](../debugger/capturecurrentframe.md)|現在のフレームの残りの部分を、グラフィックス ログ ファイルにキャプチャします。|  
|[コピー (プログラムによるキャプチャ)](../debugger/copy-programmatic-capture.md)|アクティブなグラフィックス ログ (.vsglog) ファイルの内容を、新しいファイルにコピーします。|  
|[EndCapture](../debugger/endcapture.md)|`BeginCapture` で開始されたキャプチャ区間を終了します。|  
|[Init](../debugger/init.md)|グラフィックス情報をアクティブにキャプチャして記録するように、グラフィックス診断のアプリ内コンポーネントを準備します。|  
|[ToggleHUD](../debugger/togglehud.md)|グラフィックス診断の HUD オーバーレイのオンとオフを切り替えます。|  
|[UnInit](../debugger/uninit.md)|グラフィックス ログ ファイルを終了して閉じ、アプリケーションがアクティブにグラフィックス情報を記録したときに使用されたリソースを解放します。|  
  
## <a name="remarks"></a>Remarks  
 `VsgDbg` クラスは、グラフィック診断機能をプログラムで制御するために使用できるインターフェイスを表します。 グラフィックス情報をアクティブにキャプチャおよび記録していないときでも、一部の機能を使用できます。これには、`AddMessage` メンバー関数や `ToggleHUD` メンバー関数が含まれます。 他のメンバー関数は、グラフィックス情報のアクティブなキャプチャを開始または停止するようにグラフィックス診断のアプリ内コンポーネントを準備します。または、アプリケーションがグラフィックス情報をアクティブにキャプチャしてグラフィックス ログ ファイルに記録している間に呼び出される必要があります。
