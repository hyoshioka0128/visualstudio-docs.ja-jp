---
title: ユーザー補助アプリケーションのデザイン リソース | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- accessibility, Windows applications
- Windows applications, accessibility
- Web applications, accessibility
- accessibility, Web applications
ms.assetid: 426bf023-bb34-43c4-9edb-c307191c8170
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: af300bca2b1e679eae58a92962067fcd50fea78f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297789"
---
# <a name="resources-for-designing-accessible-applications"></a>ユーザー補助アプリケーションのデザイン リソース
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザー補助 Windows アプリケーションおよび Web サイトを開発するためのヒントと例、およびユーザー補助設計をサポートする技術については、以下のリンク先を参照してください。 ユーザー補助についての一般的な情報は、Web サイト [http://www.microsoft.com/enable/](https://www.microsoft.com/accessibility/) にあります。

## <a name="technologies"></a>技術情報

- **Microsoft Active Accessibility** Microsoft Windows 上で実行するアプリケーションを開発する際に、ユーザー補助機能のサポートを向上できる COM ベースの技術です。 この技術では、ユーザー インターフェイス要素についての情報を公開するための信頼できるメソッドを提供する COM インターフェイスとアプリケーション プログラミング要素に加え、オペレーティング システムに組み込まれているダイナミック リンク ライブラリも用意されます。 詳細については、「[https://msdn.microsoft.com/library/windows/desktop/dd373592(v=vs.85).aspx](https://msdn.microsoft.com/library/windows/desktop/dd373592\(v=vs.85\).aspx)」を参照してください。

- **Microsoft .NET Speech 技術** Microsoft .NET Speech SDK は、Microsoft [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] コントロール、Microsoft Internet Explorer Speech アドイン、サンプル アプリケーション、およびドキュメントを 1 つにしたセットであり、Web 開発者はこの SDK を使って、音声対応の [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションを作成、デバッグ、および配置できます。 各ツールはシームレスに Microsoft Visual Studio と統合されるため、開発者は使い慣れた環境で開発を行うことができます。 詳細については、「[https://msdn.microsoft.com/library/ms950383.aspx](https://msdn.microsoft.com/library/ms950383.aspx)」を参照してください。

- **SAMI 1.0 の理解** Microsoft SAMI (Synchronized Accessible Media Interchange) テクノロジを利用すると、開発者は PC マルチメディアの音声コンテンツにキャプションを付けることができます。 詳細については、「[https://msdn.microsoft.com/library/ms971327.aspx](https://msdn.microsoft.com/library/ms971327.aspx)」を参照してください。

## <a name="windows-applications"></a>Windows アプリケーション

- [チュートリアル: ユーザー補助対応の Windows ベースのアプリケーションの作成](https://msdn.microsoft.com/library/654c7f2f-1586-480b-9f12-9d9b8f5cc32b) このトピックでは、Certified for Windows ロゴで必要となる、ユーザー補助機能の 5 つの要件を実装するための手順を、サンプル Windows アプリケーションを使って順番に説明します。

- [キーボード ユーザー インターフェイス デザインのガイドライン](/previous-versions/windows/desktop/dnacc/guidelines-for-keyboard-user-interface-design) この技術情報では、ユーザーがキーボードから操作できる Windows アプリケーション ユーザー インターフェイスの設計方法について説明します。

- [コンソール ユーザー補助](/previous-versions/windows/desktop/dnacc/console-accessibility) この技術情報では、ユーザー補助のサポートのために Windows XP でコンソールを表示するための API とイベントについて説明します。

## <a name="web-sites"></a>Web Sites のオフライン インストールの準備

- [チュートリアル: Image コントロール、Menu コントロール、AutoPostBack を使用する際のユーザー補助のガイドライン](https://msdn.microsoft.com/library/ff7b5021-48b3-46bf-921f-9fe1e0e32202) このトピックでは、Web 用のユーザー補助設計のヒントに加え、ユーザー補助コントロールをサンプル Web ページに含めるための手順を順番に説明します。

- [Web ページのユーザー補助機能の強化](/previous-versions/windows/desktop/dnacc/making-web-pages-more-accessible) この技術情報では、ユーザー補助機能を持つ HTML 3.2 の要素が一覧にしてあります。また、Web サイトの開発で使用してユーザー補助機能を強化するための要素も示しています。

- [ユーザー補助機能を持つ Web ページを DHTML を使って作成](/previous-versions//ms528445(v=vs.85)) この技術情報には、ユーザー補助機能を持つ HTML 4.0 要素およびユーザー補助機能を持つ Web 設計のヒントが一覧にしてあります。

- [ユーザー補助機能を持たない Web ページの代替テキスト](/previous-versions/windows/desktop/dnacc/text-alternatives-to-inaccessible-web-pages) この技術情報では、XML および XSLT を使用して、テキストのみのバージョンなど、同じ Web ページを複数の形式で表示する方法について説明しています。

### <a name="third-party-resources"></a>サードパーティのリソース

- **W3C (World Wide Web Consortium) の WAI (Web Accessibility Initiative)** この Web サイトには、ユーザー補助機能を持つ Web サイトの開発に関するガイドラインと技術情報が示されています。 詳細については、「[http://www.w3.org/WAI/GL/](https://www.w3.org/WAI/GL/)」を参照してください。

## <a name="see-also"></a>関連項目
 [Visual Studio のユーザー補助機能](../../ide/reference/accessibility-features-of-visual-studio.md)
