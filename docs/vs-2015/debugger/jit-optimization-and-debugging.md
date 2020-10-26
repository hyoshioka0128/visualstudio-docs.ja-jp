---
title: JIT の最適化とデバッグ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], optimized code
- optimized code, debugging
ms.assetid: 19bfabf3-1a2e-49dc-8819-a813982e86fd
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 56b010a01ccd7e40e696653e13dd7c972c97a9cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690534"
---
# <a name="jit-optimization-and-debugging"></a>JIT の最適化とデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マネージアプリケーションをデバッグする場合、では、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] just-in-time (JIT) コードの最適化が既定で抑制されます。 JIT 最適化の省略とは、最適化されていないコードをデバッグすることを示します。 最適化されていないため、コードの実行速度はやや遅くなりますが、デバッグで操作できる内容はより詳細になります。 最適化されたコードをデバッグするのは困難であるため、最適化されたコードで発生するバグが、非最適化バージョンでは再現しないときにのみお勧めします。  
  
 JIT の最適化は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、で [ **モジュールの読み込み時に jit 最適化を抑制** する] オプションによって制御されます。 このオプションは、[**オプション**] ダイアログボックスの [**デバッグ**] ノードの下にある [**全般**] ページで確認できます。  
  
 [ **モジュールの読み込み時に JIT 最適化を抑制** する] オプションをオフにすると、最適化された jit コードをデバッグできますが、最適化されたコードがソースコードと一致しないため、デバッグ機能が制限される可能性があります。 その結果、[ **ローカル** ] ウィンドウや [ **自動変数** ] ウィンドウなどのデバッガーウィンドウに、最適化されていないコードをデバッグする場合と同様の情報が表示されない場合があります。  
  
 もう 1 つの重要な違いは、マイ コードのみを使用したデバッグの問題です。 マイ コードのみでデバッグすると、デバッガーでは、最適化されたコードはユーザー コードではないと見なされ、これらのコードはデバッグ中に表示されません。 このため、JIT の最適化されたコードをデバッグする場合でも、マイ コードのみをオフに切り替えるという選択肢も考えられます。 詳細については、「  [マイコードのみへのステップ](../debugger/just-my-code.md#BKMK_Enable_or_disable_Just_My_Code)実行の制限」を参照してください。  
  
 モジュールの **読み込み時に JIT 最適化を抑制** するオプションでは、モジュールが読み込まれるときにコードの最適化が抑制されることに注意してください。 実行中のプロセスにアタッチする場合、既に読み込まれ、JIT でコンパイルされ、最適化されているコードが含まれることがあります。 **[モジュールの読み込み時に JIT 最適化を抑制**する] オプションは、このようなコードには影響しませんが、アタッチ後に読み込まれるモジュールに影響します。 さらに、 **[モジュールの読み込み時に JIT 最適化を抑制** する] オプションは、NGEN を使用して作成された WinForms.dll などのモジュールには影響しません。  
  
## <a name="see-also"></a>参照  
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)   
 [実行中のプロセスにアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [マネージド実行プロセス](https://msdn.microsoft.com/library/476b03dc-2b12-49a7-b067-41caeaa2f533)
