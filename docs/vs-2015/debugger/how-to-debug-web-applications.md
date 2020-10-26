---
title: '方法: Web アプリケーションをデバッグする |Microsoft Docs'
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
- Web services, debugging
- ASP.NET Web Forms, debugging
- ASP.NET, debugging Web applications
- debugging ASP.NET Web applications, during development
ms.assetid: 6440d12e-6b29-42c5-a958-99aeaaff480f
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd3cbbcd740c0f124b8ab4379204a9d425cd541c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205398"
---
# <a name="how-to-debug-web-applications"></a>方法: Web アプリケーションをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] は、で Web アプリケーションを開発するための主要なテクノロジです [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーには、ローカルまたはリモート サーバーで [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションをデバッグするための強力なツールが用意されています。 このトピックでは、開発時にプロジェクトをデバッグする方法について説明し [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ます。 実稼働サーバーに既に配置されている web アプリケーションをデバッグする方法については [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 、「 [配置済みの web アプリケーションのデバッグ](../debugger/debugging-deployed-web-applications.md)」を参照してください。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションをデバッグするには  
  
- 適切なアクセス許可が必要です。 詳細については、「 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)」をご覧ください。  
  
- [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]**プロジェクトプロパティ**でデバッグを有効にする必要があります。  
  
- アプリケーションの構成ファイル (Web.config) をデバッグ モードに設定する必要があります。 デバッグ モードの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] では、動的に生成されたファイル用のシンボルが生成され、デバッガーの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションへのアタッチが可能になります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、プロジェクトを Web プロジェクト テンプレートから作成した場合は、デバッグ開始時にこの処理が自動的に実行されます。  
  
- 詳細については、「 [方法: ASP.NET アプリケーションのデバッグを有効](../debugger/how-to-enable-debugging-for-aspnet-applications.md)にする」を参照してください。  
  
### <a name="to-debug-a-web-application-during-development"></a>開発時に Web アプリケーションをデバッグするには  
  
1. [ **デバッグ** ] メニューの [ **開始** ] をクリックして、Web アプリケーションのデバッグを開始します。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Web アプリケーションプロジェクトをビルドし、必要に応じてアプリケーションを配置します。ローカルでデバッグしている場合は ASP.NET 開発サーバーを開始し、ワーカープロセスにアタッチし [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ます。  
  
2. デバッガーを使用して、ほかのアプリケーションの場合と同様に、ブレークポイントの設定と解除、ステップの実行、およびその他のデバッグ処理を行います。  
  
     詳細については、「 [デバッガーの基本](../debugger/debugger-basics.md)」を参照してください。  
  
3. [ **デバッグ** ] メニューの [ **デバッグの停止** ] をクリックしてデバッグセッションを終了するか、Internet Explorer の [ **ファイル** ] メニューの [ **閉じる**] をクリックします。  
  
## <a name="see-also"></a>参照  
 [Web アプリケーションとスクリプトのデバッグ](../debugger/debugging-web-applications-and-script.md)   
 [ASP.NET と AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [方法: ASP.NET アプリケーションのデバッグを有効にする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
