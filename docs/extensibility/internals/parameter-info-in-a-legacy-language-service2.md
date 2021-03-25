---
title: 従来の言語でのパラメーターヒント Service2 |Microsoft Docs
description: 従来の言語サービスでメソッドが型指定されているときに、メソッドシグネチャを表示するための IntelliSense パラメーターヒント操作をサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0488c9d6570d9ed127c5b021ddfcf7d74f0dd856
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062929"
---
# <a name="parameter-info-in-a-legacy-language-service-2"></a>従来の言語サービスのパラメーターヒント2
IntelliSense パラメーターヒントは、ユーザーがメソッドパラメーターリストのパラメーターリストの開始文字 (通常は始めかっこ) を入力したときに、メソッドのシグネチャを表示するツールヒントです。 各パラメーターが入力され、パラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。

 Managed package framework (MPF) クラスは、パラメーターヒントのツールヒントを管理するための機能を提供します。 パーサーは、パラメーター start、パラメーター next、およびパラメーターの終了文字を検出する必要があり、メソッドシグネチャとそれに関連付けられたパラメーターのリストを指定する必要があります。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="implementation"></a>実装
 パーサーは、 <xref:Microsoft.VisualStudio.Package.TokenTriggers> パラメーターリストの開始文字 (多くの場合、始めかっこ) を検出したときにトリガー値が設定されるように設定する必要があります。 <xref:Microsoft.VisualStudio.Package.TokenTriggers>パラメーター区切り記号 (多くの場合、コンマ) が検出されたときにトリガーを設定する必要があります。 これにより、パラメーターヒントのツールヒントが更新され、次のパラメーターが太字で表示されます。 <xref:Microsoft.VisualStudio.Package.TokenTriggers>がパラメーターリストの末尾の文字 (多くの場合、閉じかっこ) を検出すると、パーサーはトリガーの値を設定する必要があります。

 <xref:Microsoft.VisualStudio.Package.TokenTriggers>トリガー値は、メソッドの呼び出しを開始し <xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A> ます。このメソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 解析の理由でメソッドパーサーを呼び出し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。 パラメーターリストの開始文字より前の識別子が認識されたメソッド名であるとパーサーが判断した場合、オブジェクト内の一致するメソッドシグネチャのリストを返し <xref:Microsoft.VisualStudio.Package.AuthoringScope> ます。 メソッドシグネチャが見つかった場合は、一覧の最初のシグネチャと共にパラメーターヒントのヒントが表示されます。 このツールヒントは、さらに多くの署名が入力されたときに更新されます。 パラメーターリストの終了文字を入力すると、パラメーターヒントのヒントがビューから削除されます。

> [!NOTE]
> パラメーターヒントのヒントが適切に書式設定されていることを確認するには、クラスのプロパティをオーバーライドして適切な文字を指定する必要があり <xref:Microsoft.VisualStudio.Package.Methods> ます。 基本クラスは、 <xref:Microsoft.VisualStudio.Package.Methods> C# スタイルのメソッドシグネチャを前提としています。 これを <xref:Microsoft.VisualStudio.Package.Methods> 実行する方法の詳細については、クラスを参照してください。

## <a name="enabling-support-for-the-parameter-info"></a>パラメーターヒントのサポートを有効にする
 パラメーターヒントのツールヒントをサポートするに `ShowCompletion` は、の名前付きパラメーターをに設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> `true` ます。 言語サービスは、プロパティからこのレジストリエントリの値を読み取り <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> ます。

 また、パラメーターヒントを表示するには、 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A> プロパティをに設定する必要があり `true` ます。

### <a name="example"></a>例
 パラメーターリスト文字を検出し、適切なトリガーを設定する簡単な例を次に示します。 この例は、説明を目的としたものです。 スキャナーには、 `GetNextToken` テキスト行からトークンを識別して返すメソッドが含まれていることを前提としています。 このコード例では、単純に、正しい種類の文字が表示されるたびにトリガーを設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char parameterListStartChar = '(';
        private const char parameterListEndChar   = ')';
        private const char parameterNextChar      = ',';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (Char.IsPunctuation(c))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                    tokenInfo.EndIndex = index;

                    if (c == parameterListStartChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterStart;
                    }
                    else if (c == parameterListNextChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterNext;
                    else if (c == parameterListEndChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterEnd;
                    }
                }
            return foundToken;
        }
    }
}
```

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>パーサーでパラメーターヒントのツールヒントをサポートする
 クラスは、 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.AuthoringScope> パラメーターヒント <xref:Microsoft.VisualStudio.Package.AuthoringSink> のヒントが表示および更新されるときに、クラスとクラスの内容について何らかの仮定を行います。

- パーサーは、 <xref:Microsoft.VisualStudio.Package.ParseReason> パラメーターリストの開始文字が入力されたときに指定されます。

- オブジェクトで指定された場所 <xref:Microsoft.VisualStudio.Package.ParseRequest> は、パラメーターリストの開始文字の直後にあります。 パーサーは、その位置で利用可能なすべてのメソッド宣言のシグネチャを収集し、バージョンのオブジェクトのリストに格納する必要があり <xref:Microsoft.VisualStudio.Package.AuthoringScope> ます。 この一覧には、メソッド名、メソッドの型 (または戻り値の型)、および使用可能なパラメーターの一覧が含まれています。 このリストは、後でパラメーターヒントに表示するメソッドのシグネチャまたはシグネチャを検索します。

  パーサーは、オブジェクトによって指定された行を解析し、 <xref:Microsoft.VisualStudio.Package.ParseRequest> 入力されたメソッドの名前と、ユーザーが入力するパラメーターの距離を収集する必要があります。 これを実現するには、メソッドの名前をオブジェクトのメソッドに渡し、 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> パラメーターリストの開始文字が解析されたときにメソッドを呼び出し、パラメーターリストの次の文字が解析されたときにメソッドを呼び出し、 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> 最後に <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> パラメーターリストの終了文字を解析するときにメソッドを呼び出します。 これらのメソッド呼び出しの結果は、パラメーターヒント <xref:Microsoft.VisualStudio.Package.Source> のヒントを適切に更新するためにクラスによって使用されます。

### <a name="example"></a>例
 ユーザーが入力する可能性のあるテキスト行を次に示します。 行の下の数値は、パーサーによって行のその位置でどのステップが実行されるかを示します (解析が左から右に移動することを前提としています)。 ここでは、"testfunc" メソッドシグネチャを含む、メソッドのシグネチャに対して、行の前のすべてが既に解析されていることを前提としています。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 パーサーによって実行される手順を次に示します。

1. パーサーは、 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> テキスト "testfunc" を使用してを呼び出します。

2. パーサーが <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> を呼び出します。

3. パーサーが <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> を呼び出します。

4. パーサーが <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> を呼び出します。
