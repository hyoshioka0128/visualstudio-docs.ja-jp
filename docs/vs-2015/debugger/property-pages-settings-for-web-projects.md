---
title: Web プロジェクトのプロパティページの設定 |Microsoft Docs
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
- debugging [Visual Studio], Web applications
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- debugging Web applications, project settings
- debug configurations, Web projects
ms.assetid: 8ec5160a-6408-4f47-8d41-f0e20e79a3b9
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3cb7cd3f8c3678d37feb2267f68ab5d2b3d970e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150857"
---
# <a name="property-pages-settings-for-web-projects"></a>Web プロジェクトのプロパティ ページ設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

「[デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)」で説明したように、Web サイト デバッグ構成のプロパティ設定は **[プロパティ ページ]** ダイアログ ボックスで変更できます。 次の表は、 **[プロパティ ページ]** ダイアログ ボックスのデバッガー関連の設定の場所を示しています。  
  
### <a name="configuration-properties-folder-start-options-category"></a>[構成プロパティ] フォルダー ([開始オプション] カテゴリ)  
  
|**設定**|**説明**|  
|-----------------|---------------------|  
|**開始動作**|アプリケーションの起動に関するオプション グループの見出しです。|  
|**現在のページを使用する**|デバッグの開始点として現在のページを指定します。|  
|**ページを指定する**|デバッグを開始する Web ページを指定します。|  
|**外部プログラムの開始:**|デバッグするプログラムを起動するコマンドを指定します。|  
|**コマンド ライン引数:**|上で指定したコマンドの引数を指定します。|  
|**作業ディレクトリ:**|デバッグするプログラムの作業ディレクトリを指定します。 [!INCLUDE[csprcs](../includes/csprcs-md.md)] では、作業ディレクトリはアプリケーションが起動されるディレクトリであり、既定では \bin\debug です。|  
|**URL の開始**|デバッグする Web アプリケーションの場所を指定します。|  
|**ページを開かずに外部アプリケーションからの要求を待つ**|外部のアプリケーションからの要求を待つように指示します。 このオプションは、Internet Explorer やその他のアプリケーションを起動しません。 アプリケーションから呼び出されたときにデバッグの準備をするだけです。|  
|**サーバー**|使用するサーバーに関するオプション グループの見出しです。|  
|**既定 Web サーバーを使用する**|既定の Web サーバーを使用するように指定します。|  
|**カスタム サーバーを使用する**|サーバーとして使用するベース URL を入力できます。|  
|**デバッガー**|実行するデバッグの種類に関するオプション グループの見出しです。|  
|**ASP.NET デバッグ**|[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 開発プラットフォーム用に記述されたサーバー ページのデバッグを有効にします。 **[URL の開始]** に URL を指定する必要があります。|  
|**ネイティブ コード デバッグ**|マネージド アプリケーションからネイティブ (アンマネージド) Win32 コードの呼び出しをデバッグできます。|  
|**SQL Server デバッグ**|SQL Server データベース オブジェクトのデバッグを許可します。|  
|**Silverlight デバッグ**|Silverlight コンポーネントをデバッグできます。|  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
