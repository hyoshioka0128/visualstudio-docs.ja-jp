---
title: 従来の言語サービスの機能拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- Visual Studio, language services
ms.assetid: 2700cd4d-5f68-43fc-b62f-dc80c3f3aa85
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81b5ec3de8d7b0b9466e162c3ee193c130634cd4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707408"
---
# <a name="legacy-language-service-extensibility"></a>従来の言語サービスの機能拡張
言語サービスは、IDE でソースコードを編集するための言語固有のサポートを提供します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 言語サービスを実装する新しい方法の詳細については、「[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

 このセクションでは、従来の言語サービスの構造と実装について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスの移行](../../extensibility/internals/migrating-a-legacy-language-service.md)

 言語サービスを Visual Studio 2008 から最新バージョンに更新する方法について説明します。

- [従来の言語サービスの基本情報](../../extensibility/internals/legacy-language-service-essentials.md)

 プログラミング言語を Visual Studio に統合するための言語サービスの開発方法に関する重要な情報を提供します。

- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)

 言語サービスの作成に役立つトピックへのリンクを示します。

- [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 言語サービスでの構文の強調表示のサポートについて説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 マネージ パッケージ フレームワーク (MPF) を使用して、マネージ コードでフル機能の言語サービスを実装する方法について説明します。

- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 IDE のシンボルのツリー ビューを参照できるライブラリとツールについて説明します。

## <a name="related-sections"></a>関連項目
- [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)

 Visual Studio エディターの概要について説明します。

- [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)

 プログラムのデバッグに使用するデバッガー コンポーネントの作成およびカスタマイズに必要な情報を含む Visual Studio デバッグ SDK へのリンクについて説明します。
