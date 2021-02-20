---
title: ローカライズ ツール
description: Visual Studio に含まれているローカライズ ツール、およびそれらを使用して複数の言語にローカライズされたアプリケーションを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/15/2019
ms.topic: reference
helpviewer_keywords:
- globalization [Visual Studio]
- Visual Basic code, international applications
- C#, international applications
- localization [Visual Studio]
- world-ready applications
- international applications [Visual Studio]
ms.assetid: 4d9815ae-3e80-4b4d-933d-f8309aee18d5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 77402f7503818b310a592a39706ac717ac728852
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847961"
---
# <a name="develop-globalized-and-localized-apps"></a>グローバル化およびローカライズされたアプリの開発

Visual Studio を使用すると、[.NET](/dotnet/standard/globalization-localization/) に組み込まれたサービスを活用して、海外ユーザー向けの開発を容易に行うことができます。

たとえば、Windows フォーム アプリのプロジェクト システムでは、フォールバック UI カルチャと追加のそれぞれの UI カルチャの両方のリソース ファイルを生成できます。 プロジェクトを Visual Studio でビルドする場合、リソース ファイルは Visual Studio XML 形式 (.resx) から中間バイナリ形式 (.resources) にコンパイルされ、その後、サテライト アセンブリに埋め込まれます。 詳細については、「[Resource files in Visual Studio](/dotnet/framework/resources/creating-resource-files-for-desktop-apps#VSResFiles)」 (Visual Studio のリソース ファイル) と「[デスクトップ アプリケーションに対するサテライト アセンブリの作成](/dotnet/framework/resources/creating-satellite-assemblies-for-desktop-apps)」を参照してください。

## <a name="bidirectional-languages"></a>双方向言語

Visual Studio では、アラビア語やヘブライ語など、右から左に書く言語で正しくテキストが表示されるアプリケーションを作成できます。 いくつかの機能については、単にプロパティを設定するだけで済みます。 それ以外の場合は、コードで機能を実装する必要があります。

> [!NOTE]
> 双方向言語を入力したり表示したりするには、適切な言語に設定されたバージョンの Windows を使用する必要があります。 英語バージョンの Windows に適切な Language Pack をインストールする方法と、適切にローカライズされたバージョンの Windows を使用する方法があります。

### <a name="apps-that-support-bidirectional-languages"></a>双方向言語をサポートするアプリ

- Windows アプリ

   双方向テキスト、右から左への読み取り順序、およびミラー化 (ウィンドウ、メニュー、ダイアログ ボックスなどのレイアウトの反転) をサポートする、完全な双方向アプリケーションを作成できます。 ミラー化を除き、これらの機能は、既定またはプロパティ設定により使用できるようになっています。 ミラー化は、メッセージ ボックスなどいくつかの機能に対してはあらかじめサポートされています。 ただし、それ以外の場合には、ミラー化をコードで実装する必要があります。 詳細については、「[Windows フォーム アプリケーションの双方向サポート](/dotnet/framework/winforms/advanced/bi-directional-support-for-windows-forms-applications)」をご覧ください。

- Web アプリ

   Web サービスは UTF-8 および Unicode のテキストの送受信をサポートしているため、双方向言語を使用するアプリケーションに適しています。 Web クライアント アプリケーションのユーザー インターフェイスはブラウザーに依存しているため、Web アプリケーションでの双方向サポートの内容は、ユーザーのブラウザーが双方向機能をどの程度サポートしているかによって異なります。 Visual Studio では、アラビア語またはヘブライ語のテキスト、右から左への読み取り順序、ファイルのエンコーディング、およびローカル カルチャ設定をサポートするアプリケーションを作成できます。 詳しくは、「[ASP.NET Web アプリケーションに対する双方向サポート](/previous-versions/6eedwbtt(v=vs.140))」をご覧ください。

> [!NOTE]
> コンソール アプリでは、双方向言語のテキストがサポートされません。 これは、Windows におけるコンソール アプリケーションの動作のしくみによるものです。

## <a name="see-also"></a>関連項目

- [Visual Studio での双方向言語のサポート](use-bidirectional-languages.md)
- [.NET アプリのグローバル化とローカライズ](/dotnet/standard/globalization-localization/)
- [.NET アプリのリソース](/dotnet/framework/resources/)