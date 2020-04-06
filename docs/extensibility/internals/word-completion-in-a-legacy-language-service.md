---
title: レガシー言語サービスでの単語補完 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 948751cde5b6b710d911a30ca26a61e5411bba4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703173"
---
# <a name="word-completion-in-a-legacy-language-service"></a>従来の言語サービスでの単語補完
単語補完は、部分的に入力された単語の欠落している文字を埋めます。 完了可能な入力が 1 つだけの場合は、入力時に単語が完了します。 部分単語が複数の可能性に一致する場合は、候補の一覧が表示されます。 完了文字は、識別子に使用されない任意の文字にすることができます。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[エディタと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation-steps"></a>実装手順

1. ユーザーが**IntelliSense**メニューから**完全な単語**を選択すると<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>、コマンドが言語サービスに送信されます。

2. この<xref:Microsoft.VisualStudio.Package.ViewFilter>クラスはコマンドをキャッチし、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>の解析理由を使用<xref:Microsoft.VisualStudio.Package.ParseReason>してメソッドを呼び出します。

3. 次<xref:Microsoft.VisualStudio.Package.Source>に、このクラス<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>はメソッドを呼び出して、可能な単語補完のリストを取得し、クラスを使用して<xref:Microsoft.VisualStudio.Package.CompletionSet>ツール ヒント リストに単語を表示します。

    一致する単語が 1 つだけ<xref:Microsoft.VisualStudio.Package.Source>の場合、クラスは単語を完成させます。

   または、識別子の最初の文字が入力されたときに<xref:Microsoft.VisualStudio.Package.TokenTriggers>スキャナーがトリガ値を返す場合、<xref:Microsoft.VisualStudio.Package.Source>クラスはこれを検出し、解析理由を<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>指定してメソッドを呼び出<xref:Microsoft.VisualStudio.Package.ParseReason>します。 この場合、パーサーはメンバー選択文字の存在を検出し、メンバーのリストを提供する必要があります。

## <a name="enabling-support-for-the-complete-word"></a>完全な単語のサポートを有効にする
 単語補完のサポートを有効にするには、`CodeSense`言語パッケージに関連付<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>けられたユーザー属性に渡される名前付きパラメーターを設定します。 これにより、クラス<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>のプロパティが<xref:Microsoft.VisualStudio.Package.LanguagePreferences>設定されます。

 パーサーは、ワード完了が動作するために、解析理由値<xref:Microsoft.VisualStudio.Package.ParseReason>に応答して宣言のリストを返す必要があります。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>解析ソース メソッドで完全な単語を実装する
 単語補完の場合、<xref:Microsoft.VisualStudio.Package.Source>クラスはクラス<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>のメソッドを<xref:Microsoft.VisualStudio.Package.AuthoringScope>呼び出して、一致する可能性のある単語のリストを取得します。 リストは、クラスから派生したクラスで実装する<xref:Microsoft.VisualStudio.Package.Declarations>必要があります。 実装する<xref:Microsoft.VisualStudio.Package.Declarations>必要があるメソッドの詳細については、クラスを参照してください。

 リストに単語が 1 つだけ含まれている場合<xref:Microsoft.VisualStudio.Package.Source>、クラスは単語の一部の代わりに自動的にその単語を挿入します。 リストに複数の単語が含まれている場合、<xref:Microsoft.VisualStudio.Package.Source>クラスはツール ヒント リストを表示し、ユーザーが適切な選択肢を選択できます。

 また、「<xref:Microsoft.VisualStudio.Package.Declarations>[レガシー言語サービスのメンバー完了」で](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)のクラス実装の例も参照してください。
