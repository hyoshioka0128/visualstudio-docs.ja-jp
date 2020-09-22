---
title: デプロイされた Web アプリケーションのデバッグ |Microsoft Docs
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
- ASP.NET Web applications
- Web services, debugging
- XML, debugging Web services
- debugging Web services
- ASP.NET, debugging Web applications
- XML Web services, debugging
ms.assetid: b938a91b-be96-416f-83bc-4177e7f3929a
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9608643801255d6c2cbf278cbfd96908f1f3911d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842237"
---
# <a name="debugging-deployed-web-applications"></a>配置した Web アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

運用サーバーで実行されている Web アプリケーションをデバッグする場合は、慎重に行う必要があります。 たとえば、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスにアタッチしてデバッグを行い、ブレークポイントにヒットした場合、そのワーカー プロセス内のすべてのマネージド コードが停止します。 ワーカー プロセス内のすべてのマネージド コードが停止すると、サーバーのすべてのユーザーの業務が停止する可能性があります。 運用サーバーでデバッグする場合は、事前に、実際の業務への影響について検討する必要があります。  
  
 配置されたアプリケーションを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用してデバッグするには、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスにアタッチし、デバッガーからアプリケーションのシンボルにアクセスできるようにする必要があります。 また、アプリケーションのソース ファイルを見つけて開く必要があります。 詳細については、「[シンボル (.pdb) とソース ファイルを指定する](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」、「[方法: ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)」、および「[システム要件](../debugger/aspnet-debugging-system-requirements.md)」を参照してください。  
  
> [!NOTE]
> 多くの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションは、ビジネス ロジックまたはその他の有用なコードが格納されている DLL を参照します。 このような参照では、ローカル コンピューターにある DLL が自動的に Web アプリケーションの仮想ディレクトリの \bin フォルダーにコピーされます。 デバッグ時には、Web アプリケーションが、ローカル コンピューターの DLL ではなく、仮想ディレクトリにある DLL のコピーを参照している点に注意してください。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスにアタッチする方法は、他のリモート プロセスにアタッチする場合と同じです。 アタッチしたときに正しいプロジェクトが開いていない場合、アプリケーションが中断するとダイアログ ボックスが表示されます。 このダイアログ ボックスでは、アプリケーションのソース ファイルの場所を指定するように求められます。 このダイアログ ボックスに指定するファイル名は、Web サーバー上のデバッグ シンボルで指定されているファイル名と一致する必要があります。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [ASP.NET と AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [Web アプリケーションとスクリプトのデバッグ](../debugger/debugging-web-applications-and-script.md)   
 [方法: ASP.NET アプリケーションのデバッグを有効にする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)   
 [方法: ASP.NET プロセスの名前を検索する](../debugger/how-to-find-the-name-of-the-aspnet-process.md)   
 [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
