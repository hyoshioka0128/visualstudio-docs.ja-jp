---
title: リモート コンピューターにアクセスしようとしたときに、DCOM エラーが発生しました。 アクセスが拒否されました。 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.dcom_access_denied
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, DCOM error
- remote DCOM access denied error
- DCOM, access errors
ms.assetid: 9d7dfc1b-9fe0-4f54-9c50-9c0e0f8358c5
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0157b1ade2c38a2c10920b9674d7c9a58ac036b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156530"
---
# <a name="a-dcom-error-occurred-trying-to-contact-the-remote-computer-access-is-denied"></a>リモート コンピューターにアクセスしようとしたときに、DCOM エラーが発生しました。 アクセスが拒否されました。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リモート デバッグでは、DCOM を使用して次のような状況でローカル コンピューターとリモート コンピューターとの間で通信します。  
  
- デバッガーが**ネイティブ互換モード**に設定されているか、[**ツール]、[オプション]** 、[デバッグ] ページで [**マネージ互換モード**] がオンになっています。  
  
- マネージド C++ (C + +/CLI) コードをデバッグする場合。  
  
- Visual Studio 2013 で、[**ツール]/[オプション]/[デバッグ**] ページで [ネイティブの**エディットコンティニュを有効に**する] チェックボックスがオンになっている場合  
  
- 一部のサード パーティのデバッグ シナリオ  
  
  このエラーが発生するのは、Visual Studio のプロセスが DCOM 経由でリモート デバッガープロセスに対して自己認証できない (入力した資格情報が不十分と見なされた) 場合です。 次のいずれかの回避策で問題を解決できることがあります。  
  
- **[ネイティブ互換モード]** と **[マネージド互換モード]** をオフにします。  
  
- Visual Studio 2013 で、 **[ネイティブのエディット コンティニュを有効にする]** をオフにします。  
  
- 両方のコンピューターを再起動する。  
  
- リモート デバッグで資格情報の入力が必要な場合は、資格情報の保存のチェック ボックスをオンにする。  
  
## <a name="see-also"></a>参照  
 [リモートデバッグエラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Remote Debugging](../debugger/remote-debugging.md)
