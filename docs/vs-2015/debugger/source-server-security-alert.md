---
title: ソース サーバーのセキュリティ警告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.enablewarning
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 8451c281-6914-469c-b80c-6271cc3f3d17
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f8b122deab5dbdc30b129bce221a804f8c53aa3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699322"
---
# <a name="source-server-security-alert"></a>ソース サーバー のセキュリティ警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソース サーバーの使用時は、認識できて信頼できる場所からのシンボル ファイルのみを使用してください。  
  
 ソース サーバーのサポートを有効にすると、この警告が表示されます。 ソース サーバーのコマンドは、デバッグ シンボル ファイル (PDB ファイル) に埋め込まれています。 PDB ファイルの作成元を確認してください。  
  
> [!IMPORTANT]
> ソース サーバーを使用する場合、次の潜在的なセキュリティ上の脅威について考慮する必要があります。アプリケーションの PDB ファイルには任意のコマンドを埋め込むことができるため、srcsrv.ini ファイルには実行するコマンドのみ配置するようにします。 srcsvr.ini ファイルにないコマンドを実行しようとすると、確認のダイアログ ボックスが表示されます。 詳細については、「 [セキュリティの警告: デバッガーは信頼されていないコマンドを実行する必要があり](../debugger/security-warning-debugger-must-execute-untrusted-command.md)ます。コマンドパラメーターに対して検証は行われないので、信頼されたコマンドに注意してください。 たとえば、cmd.exe を信頼した場合、悪意のあるユーザーが危険な動作を実行するようにコマンドにパラメーターを指定する可能性があります。  
  
## <a name="see-also"></a>参照  
 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [ソース サーバー](https://msdn.microsoft.com/library/windows/desktop/ms680641.aspx)
