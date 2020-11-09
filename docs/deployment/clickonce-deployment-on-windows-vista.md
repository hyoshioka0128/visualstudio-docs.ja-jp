---
title: Windows Vista の ClickOnce 配置 |Microsoft Docs
description: Visual Studio が ClickOnce および Registration-Free COM アプリケーションの外部 UAC マニフェストを生成する方法について説明します。外部のマニフェストが必要です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2e09225339a87c55c31d27d26b129e199385e99
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94383080"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista の ClickOnce 配置

Windows Vista のユーザーアカウント制御 (UAC) 用に Visual Studio でアプリケーションをビルドすると、通常、アプリケーションの実行可能ファイルにバイナリ XML データとしてエンコードされた埋め込みマニフェストが生成されます。  ClickOnce および Registration-Free COM アプリケーションには外部マニフェストが必要であるため、Visual Studio では、埋め込みマニフェストではなく、UAC データを含むこれらのプロジェクト用のファイルが生成されます。 ClickOnce および Registration-Free COM 配置では、Visual Studio は、 *app.xaml* と呼ばれるファイルからの情報を使用して、外部の UAC マニフェスト情報を生成します。 それ以外の場合は、Visual Studio によって、UAC データがアプリケーションの実行可能ファイルに埋め込まれます。

Visual Studio には、マニフェスト生成のための次のオプションが用意されています。

- 埋め込みマニフェストを使用します。 UAC データをアプリケーションの実行可能ファイルに埋め込み、通常のユーザーとして実行します。

   これは既定の設定です (ClickOnce を使用している場合を除く)。 この設定は、Visual Studio が Windows Vista で動作する通常の方法をサポートしています。また、を使用して内部マニフェストと外部マニフェストの両方を生成し `AsInvoker` ます。

- 外部マニフェストを使用します。 *アプリケーションマニフェスト* を使用して外部マニフェストを生成します。

   これにより、 *アプリケーションマニフェスト* の情報を使用して、外部マニフェストのみが生成されます。 ClickOnce または Registration-Free COM を使用してアプリケーションを発行すると、Visual Studio によってプロジェクトに *app.xaml* が追加され、このオプションが追加されます。

- マニフェストを使用しません。 マニフェストを使用せずにアプリケーションを作成します。

   この方法は、 *仮想化* とも呼ばれます。 以前のバージョンの Visual Studio の既存のアプリケーションとの互換性を確保するには、このオプションを使用します。

  新しいプロパティは、プロジェクトデザイナーの [ **アプリケーション** ] ページ (Visual C# プロジェクトの場合のみ) と MSBuild プロジェクトファイル形式で使用できます。

  Visual Studio IDE で UAC マニフェストの生成を構成する方法は、プロジェクトの種類 (Visual C# または Visual Basic) によって異なります。

  * マニフェスト生成のための Visual C# プロジェクトの構成の詳細については、「 [[アプリケーション] ページ (プロジェクトデザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)」を参照してください。

  * マニフェスト生成のための Visual Basic プロジェクトの構成の詳細については、「 [[アプリケーション] ページ (プロジェクトデザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ユーザーアクセス許可と Visual Studio](/previous-versions/ms165100(v=vs.100))
- [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md)