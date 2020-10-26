---
title: Windows Vista の ClickOnce 配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- UAC manifest generation
- ClickOnce deployment, Windows
- manifest generation
- Windows, ClickOnce deployment
ms.assetid: b21a0ebc-0ff6-4f49-8993-7d1ad3f8cac2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e25f9da960b1de8acb1950b2bdd3ab7e61409f17
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675473"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista の ClickOnce 配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Vista のユーザーアカウント制御 (UAC) 用に Visual Studio でアプリケーションをビルドすると、通常、アプリケーションの実行可能ファイルにバイナリ XML データとしてエンコードされた埋め込みマニフェストが生成されます。 ClickOnce および登録を必要としない COM アプリケーションには外部マニフェストが必要であるため、Visual Studio では、埋め込みマニフェストではなく、UAC データを含むこれらの種類のプロジェクトのファイルが生成されます。 既定では、Visual Studio は、app.xaml と呼ばれるファイルからの情報を使用して、外部の UAC マニフェスト情報 (ClickOnce および登録を必要としない COM 配置用) を生成するか、アプリケーションの実行可能ファイルに埋め込みます (他のすべての場合)。 Visual Studio には、マニフェスト生成のための次のオプションが用意されています。  
  
- 埋め込みマニフェストを使用します。 UAC データをアプリケーションの実行可能ファイルに埋め込み、通常のユーザーとして実行します。  
  
   これは既定の設定です (ClickOnce を使用している場合を除く)。 この設定は、Visual Studio が Windows Vista で動作する通常の方法をサポートします。つまり、を使用して、内部マニフェストと外部マニフェストの両方を生成し `AsInvoker` ます。  
  
- 外部マニフェストを使用します。 アプリケーションマニフェストを使用して外部マニフェストを生成します。  
  
   これにより、アプリケーションマニフェストの情報を使用して、外部マニフェストのみが生成されます。 ClickOnce または登録を必要としない COM を使用してアプリケーションを発行すると、Visual Studio によってプロジェクトに .manifest が追加され、このオプションが追加されます。  
  
- マニフェストを使用しません。 マニフェストを使用せずにアプリケーションを作成します。  
  
   この方法は、 *仮想化*とも呼ばれます。 以前のバージョンの Visual Studio の既存のアプリケーションとの互換性を確保するには、このオプションを使用します。  
  
  新しいプロパティは、プロジェクトデザイナーの [ **アプリケーション** ] ページ (Visual C# プロジェクトの場合のみ) と MSBuild プロジェクトファイル形式で使用できます。  
  
  Visual Studio IDE で UAC マニフェストの生成を構成する方法は、プロジェクトの種類 (Visual C# と Visual Basic) によって異なります。  
  
  マニフェスト生成のための Visual C# プロジェクトの構成の詳細については、「 [[アプリケーション] ページ (プロジェクトデザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)」を参照してください。  
  
  マニフェスト生成のための Visual Basic プロジェクトの構成の詳細については、「 [[アプリケーション] ページ (プロジェクトデザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [ユーザーアクセス許可と Visual Studio](https://msdn.microsoft.com/d5c55084-1e7b-4b61-b478-137db01c0fc0)   
 [[アプリケーション] ページ (プロジェクトデザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)   
 [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md)
