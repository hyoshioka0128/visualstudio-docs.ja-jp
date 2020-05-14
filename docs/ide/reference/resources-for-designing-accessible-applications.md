---
title: ユーザー補助アプリケーションのデザイン リソース
description: 障碍を持つユーザーが使いやすいアプリケーションを作成する方法をについて説明します。
ms.date: 08/27/2019
ms.topic: conceptual
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
helpviewer_keywords:
- accessibility, Windows applications
- Windows applications, accessibility
- Web applications, accessibility
- accessibility, Web applications
ms.assetid: 426bf023-bb34-43c4-9edb-c307191c8170
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8ac7beac67a2f1d0010ee64ae7af31108d7ec3b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "70107847"
---
# <a name="resources-for-designing-accessible-applications"></a>ユーザー補助アプリケーションのデザイン リソース

アクセシビリティ対応のデザインをサポートするテクノロジについて説明します。 また、アクセシビリティ対応の Windows アプリと Web サイトを開発するのに役立つヒントとチュートリアルへのリンクも含まれています。

>[!NOTE]
>すべてのユーザーを支援する製品の開発方法の詳細については、[Microsoft Accessibility](https://www.microsoft.com/accessibility/) を参照してください。

## <a name="technologies"></a>テクノロジ

* **Microsoft Active Accessibility** Microsoft Windows 上で実行するアプリケーションを開発する際に、ユーザー補助機能のサポートを向上できる COM ベースの技術です。 オペレーティング システムおよび COM インターフェイスに組み込まれているダイナミック リンク ライブラリが提供されます。 また、ユーザー インターフェイス要素に関する情報を公開するためのメソッドを提供するアプリケーション プログラミング要素もあります。 詳細については、「[Microsoft Active Accessibility](/windows/desktop/WinAuto/microsoft-active-accessibility)」をご覧ください。

* **Microsoft .NET Speech 技術** Microsoft .NET Speech SDK では、Microsoft [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] コントロール、Microsoft Internet Explorer Speech アドイン、サンプル アプリケーション、およびドキュメントのセットが提供されます。 Web 開発者は、これらのツールを使って、音声対応の [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] アプリケーションを作成、デバッグ、配置できます。 ツールは Microsoft Visual Studio とシームレスに統合されるため、開発者は使い慣れた開発環境で作業することができます。 詳細については、「[Speech Server](/previous-versions/office/developer/speech-technologies/ms950383\(v\=msdn.10\))」をご覧ください。

* **SAMI 1.0 の理解** Microsoft SAMI (Synchronized Accessible Media Interchange) テクノロジを利用すると、開発者は PC マルチメディアの音声コンテンツにキャプションを付けることができます。 詳細については、「[SAMI 1.0 の理解](/previous-versions/windows/desktop/dnacc/understanding-sami-1.0)」を参照してください。

## <a name="windows-applications"></a>Windows アプリケーション

* **[チュートリアル: ユーザー補助対応の Windows ベースのアプリケーションの作成](/dotnet/framework/winforms/advanced/walkthrough-creating-an-accessible-windows-based-application)** この記事では、Certified for Windows ロゴで必要となる、ユーザー補助機能の 5 つの要件を実装するための手順を、サンプル Windows アプリケーションを使って順番に説明します。

* **キーボード ユーザー インターフェイス デザインのガイドライン** この技術情報では、ユーザーがキーボードから操作できる Windows アプリケーションの設計方法について説明します。 詳細については、「[Guidelines for keyboard user interface design](/previous-versions/windows/desktop/dnacc/guidelines-for-keyboard-user-interface-design)」(キーボード ユーザー インターフェイス設計のガイドライン) をご覧ください。

* **コンソール ユーザー補助** この技術情報では、ユーザー補助のサポートのために Windows XP でコンソールを表示するための API とイベントについて説明します。 詳細については、「[Console accessibility](/previous-versions/windows/desktop/dnacc/console-accessibility)」(コンソールのユーザー補助) をご覧ください。

## <a name="websites"></a>Websites

- [チュートリアル: Image コントロール、Menu コントロール、AutoPostBack を使用する際のユーザー補助のガイドライン](https://msdn.microsoft.com/Library/ff7b5021-48b3-46bf-921f-9fe1e0e32202) この記事では、ユーザー補助コントロールをサンプル Web ページに含めるための手順を説明します。 Web 用のユーザー補助設計のヒントも示します。

- **ユーザー補助機能を持つ Web ページを DHTML を使って作成** この技術情報には、ユーザー補助機能を持つ HTML 4.0 要素およびユーザー補助機能を持つ Web 設計のヒントが一覧にしてあります。 詳細については、「[Create accessible web pages with DHTML](https://msdn.microsoft.com/library/ms528445.aspx)」(ユーザー補助機能を持つ Web ページを DHTML で作成する) をご覧ください。

### <a name="third-party-resources"></a>サードパーティのリソース

- **W3C (World Wide Web Consortium) の WAI (Web Accessibility Initiative)** この Web サイトには、ユーザー補助機能を持つ Web サイトの開発に関するガイドラインと技術情報が示されています。 詳細については、[https://www.w3.org/WAI/GL/](https://www.w3.org/WAI/GL/) を参照してください。

## <a name="see-also"></a>参照

* [Visual Studio のユーザー補助機能](../../ide/reference/accessibility-features-of-visual-studio.md)
* [Visual Studio for Mac のユーザー補助](/visualstudio/mac/accessibility/)
