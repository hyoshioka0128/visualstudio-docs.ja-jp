---
title: デバッグとホスティング プロセス | Microsoft Docs
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
- debugging [Visual Studio], hosting process
- hosting process
ms.assetid: d0f0b9a6-2a6e-463d-b6ea-9518ee727933
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 10f3968367b188203671fa6bfff48bc482efe4f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157894"
---
# <a name="debugging-and-the-hosting-process"></a>プロセスのデバッグとホスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のホスティング プロセスでは、デバッガーのパフォーマンスを向上させ、部分信頼のデバッグやデザイン時の式の評価など、新しいデバッガー機能が使用できるようになりました。 必要に応じてホスティング プロセスを無効にすることもできます。 詳細については、「 [How to: Disable the Hosting Process](../ide/how-to-disable-the-hosting-process.md)」を参照してください。 次のセクションでは、ホスティング プロセスがある場合とない場合のデバッグの違いについて説明します。  
  
## <a name="partial-trust-debugging-and-click-once-security"></a>部分信頼のデバッグと ClickOnce のセキュリティ  
 部分信頼のデバッグにはホスティング プロセスが必要です。 ホスティング プロセスを無効にすると、 **[プロジェクトのプロパティ]** の **[セキュリティ]** ページで部分信頼が有効になっている場合でも、部分信頼のデバッグは機能しません。 詳細については、次のトピックを参照してください。 [How to: Disable the Hosting Process](../ide/how-to-disable-the-hosting-process.md) および [How to: Debug a Partial Trust Application](../debugger/how-to-debug-a-partial-trust-application.md).  
  
## <a name="design-time-expression-evaluation"></a>デザイン時の式評価  
 デザイン時の式では、常にホスティング プロセスが使用されます。 **[プロジェクトのプロパティ]** でホスティング プロセスを無効にすると、クラス ライブラリ プロジェクトでデザイン時の式の評価も無効になります。 他のプロジェクトの種類では、デザイン時の式の評価は無効になりません。 代わりに、Visual Studio で実際の実行可能ファイルが起動され、ホスティング プロセスを使用せずにデザイン時の評価に使用されます。 この違いがあるため、結果も異なる可能性があります。  
  
## <a name="appdomaincurrentdomainfriendlyname-differences"></a>AppDomain.CurrentDomain.FriendlyName の違い  
 `AppDomain.CurrentDomain.FriendlyName` は、ホスティング プロセスが有効かどうかによって異なる結果を返します。 ホスティング プロセスを有効にして `AppDomain.CurrentDomain.FriendlyName` を呼び出すと、 *app_name*`.vhost.exe`が返されます。 ホスティング プロセスを無効にして呼び出した場合は、 *app_name*`.exe`が返されます。  
  
## <a name="assemblygetcallingassemblyfullname-differences"></a>Assembly.GetCallingAssembly().FullName の違い  
 `Assembly.GetCallingAssembly().FullName` は、ホスティング プロセスが有効かどうかによって異なる結果を返します。 ホスティング プロセスを有効にして `Assembly.GetCallingAssembly().FullName` を呼び出すと、 `mscorlib`が返されます。 ホスティング プロセスを無効にして `Assembly.GetCallingAssembly().FullName` を呼び出すと、アプリケーション名が返されます。  
  
## <a name="see-also"></a>参照  
 [ホストプロセス (vshost.exe)](../ide/hosting-process-vshost-exe.md)   
 [方法: 部分信頼アプリケーションをデバッグする](../debugger/how-to-debug-a-partial-trust-application.md)   
 [方法: ホストプロセスを無効にする](../ide/how-to-disable-the-hosting-process.md)
