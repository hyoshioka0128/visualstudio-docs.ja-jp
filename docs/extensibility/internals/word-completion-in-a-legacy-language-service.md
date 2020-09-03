---
title: 従来の言語サービスでの単語補完 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703173"
---
# <a name="word-completion-in-a-legacy-language-service"></a>従来の言語サービスでの単語補完
単語入力補完は、部分的に入力された単語の不足している文字を入力します。 候補が1つしかない場合は、入力候補文字が入力されると、その単語が完成します。 単語の一部が複数の可能性に一致する場合、候補の一覧が表示されます。 完了文字には、識別子に使用されない任意の文字を指定できます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="implementation-steps"></a>実装手順

1. ユーザーが**IntelliSense**メニューから [ **Complete Word** ] を選択すると、 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドが言語サービスに送信されます。

2. クラスは、 <xref:Microsoft.VisualStudio.Package.ViewFilter> コマンドをキャッチし、 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> の解析の理由でメソッドを呼び出し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。

3. <xref:Microsoft.VisualStudio.Package.Source>次に、クラスはメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 使用可能な単語入力候補の一覧を取得し、クラスを使用して、ツールヒントの一覧に単語を表示し <xref:Microsoft.VisualStudio.Package.CompletionSet> ます。

    一致する単語が1つしかない場合、 <xref:Microsoft.VisualStudio.Package.Source> クラスは単語を完了します。

   また、 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 識別子の最初の文字が入力されたときにスキャナーがトリガーの値を返す場合、 <xref:Microsoft.VisualStudio.Package.Source> クラスはこれを検出し、 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> の解析の理由でメソッドを呼び出し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。 この場合、パーサーはメンバー選択文字の存在を検出し、メンバーの一覧を提供する必要があります。

## <a name="enabling-support-for-the-complete-word"></a>入力候補のサポートを有効にする
 Word 入力候補のサポートを有効にするには、 `CodeSense` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 言語パッケージに関連付けられたユーザー属性に渡される名前付きパラメーターを設定します。 これにより、クラスのプロパティが設定され <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences> ます。

 ワードコンプリートを操作するには、解析の理由値に応じて、パーサーが宣言の一覧を返す必要があり <xref:Microsoft.VisualStudio.Package.ParseReason> ます。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>ParseSource メソッドに Complete Word を実装する
 単語の補完のために、クラスはクラスのメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> 単語の一致候補のリストを取得します。 クラスから派生したクラスにリストを実装する必要があり <xref:Microsoft.VisualStudio.Package.Declarations> ます。 実装する <xref:Microsoft.VisualStudio.Package.Declarations> 必要のあるメソッドの詳細については、クラスを参照してください。

 リストに1つの単語だけが含まれている場合、クラスは、 <xref:Microsoft.VisualStudio.Package.Source> その単語を部分語の代わりに自動的に挿入します。 リストに複数の単語が含まれている場合、クラスは、 <xref:Microsoft.VisualStudio.Package.Source> ユーザーが適切な選択を選択できるツールヒントリストを提示します。

 また、「 <xref:Microsoft.VisualStudio.Package.Declarations> [従来の言語サービスでのメンバー入力候補](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)」にあるクラス実装の例も参照してください。
