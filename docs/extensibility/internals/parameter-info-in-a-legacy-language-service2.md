---
title: レガシー言語サービスのパラメータ情報2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e2c40c9ca5c038a70714545f4133db0c0dd686d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706741"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>従来の言語サービスのパラメーター ヒント
IntelliSense パラメーター ヒントは、ユーザーがメソッド パラメーター リスト リストの開始文字 (通常は左かっこ) を入力したときにメソッドのシグネチャを表示するツールヒントです。 各パラメーターが入力され、パラメーター区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。

 管理パッケージ フレームワーク (MPF) クラスは、パラメーターヒントの管理をサポートします。 パーサーは、パラメーター開始、パラメーターの次のパラメーター、およびパラメーターの終了文字を検出する必要があり、メソッドシグネチャとそれに関連付けられたパラメーターのリストを指定する必要があります。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[エディタと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation"></a>実装
 パーサーは、パラメーター・リストの<xref:Microsoft.VisualStudio.Package.TokenTriggers>開始文字 (多くの場合、左括弧) を見つけたときに、トリガー値が設定されるように設定する必要があります。 パラメーター区切<xref:Microsoft.VisualStudio.Package.TokenTriggers>り記号 (多くの場合コンマ) が見つかったときにトリガーを設定する必要があります。 これにより、パラメーターヒントツールが更新され、次のパラメーターが太字で表示されます。 パーサーは、パラメーター・リストの<xref:Microsoft.VisualStudio.Package.TokenTriggers>終了文字 (しばしば閉じ括弧) が見つかった場合に、トリガー値を設定する必要があります。

 トリガー<xref:Microsoft.VisualStudio.Package.TokenTriggers>値はメソッドの呼び出し<xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A>を開始し、メソッドパーサーを<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>解析理由で呼び出<xref:Microsoft.VisualStudio.Package.ParseReason>します。 パーサーは、パラメーター リストの開始文字の前の識別子が認識されたメソッド名であると判断した場合、オブジェクト内の一致するメソッド<xref:Microsoft.VisualStudio.Package.AuthoringScope>シグネチャのリストを返します。 メソッドシグネチャが見つかった場合は、リストの最初のシグネチャを含む [パラメータ情報] ツールチップが表示されます。 このツールヒントは、署名の詳細が入力されると更新されます。 パラメーター リストの終了文字を入力すると、[パラメーターヒント] ツールチップがビューから削除されます。

> [!NOTE]
> パラメーターヒントのツールヒントが正しく書式設定されていることを確認するには、<xref:Microsoft.VisualStudio.Package.Methods>クラスのプロパティをオーバーライドして、適切な文字を指定する必要があります。 基本<xref:Microsoft.VisualStudio.Package.Methods>クラスは、C# スタイルのメソッド シグネチャを想定しています。 これを行<xref:Microsoft.VisualStudio.Package.Methods>う方法の詳細については、クラスを参照してください。

## <a name="enabling-support-for-the-parameter-info"></a>パラメーター情報のサポートの有効化
 パラメーターヒントツールヒントをサポートするには、 の`ShowCompletion`名前付きパラメーター<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>を`true`に設定する必要があります。 言語サービスは、プロパティからこのレジストリ エントリの値<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>を読み取ります。

 さらに、パラメーターヒント<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A>を表示するには、プロパティ`true`を に設定する必要があります。

### <a name="example"></a>例
 ここでは、パラメータリスト文字を検出し、適切なトリガを設定する簡単な例を示します。 この例は、説明のみを目的とします。 この例では、スキャナーに、テキスト`GetNextToken`行からトークンを識別して返すメソッドが含まれていることを前提としています。 このコード例では、適切な種類の文字が見えたときにトリガを設定します。

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

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>パーサーでのパラメーター情報ツールヒントのサポート
 クラス<xref:Microsoft.VisualStudio.Package.Source>は、パラメーターヒントのツールヒントが表示および<xref:Microsoft.VisualStudio.Package.AuthoringScope>更新<xref:Microsoft.VisualStudio.Package.AuthoringSink>されたときに、 および クラスの内容についていくつかの前提を作成します。

- パーサーは、パラメーター <xref:Microsoft.VisualStudio.Package.ParseReason> ・リストの開始文字を入力するときに指定されます。

- オブジェクト内で指定された<xref:Microsoft.VisualStudio.Package.ParseRequest>位置は、パラメーター・リストの開始文字の直後にあります。 パーサーは、その位置で使用可能なすべてのメソッド宣言のシグネチャを収集し、オブジェクトのバージョンのリストに格納する<xref:Microsoft.VisualStudio.Package.AuthoringScope>必要があります。 このリストには、メソッド名、メソッドの型 (または戻り値の型)、および使用可能なパラメーターの一覧が含まれています。 このリストは、後で[パラメータ情報]ツールチップに表示するメソッドシグネチャまたはシグネチャを検索します。

  パーサーは、オブジェクトによって指定された行を<xref:Microsoft.VisualStudio.Package.ParseRequest>解析して、入力されるメソッドの名前と、ユーザーがパラメーターを入力する距離を収集する必要があります。 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>これは、<xref:Microsoft.VisualStudio.Package.AuthoringSink>メソッドの名前をオブジェクトのメソッドに渡し、パラメーター リストの開始文字が<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>解析されるときに<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>メソッドを呼び出し、次のパラメーター リストが解析されるときにメソッドを呼び出し、最後にパラメーター<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>リスト終了文字が解析されるときにメソッドを呼び出すことで実現されます。 これらのメソッド呼び出しの結果は、<xref:Microsoft.VisualStudio.Package.Source>パラメーターヒントを適切に更新するためにクラスによって使用されます。

### <a name="example"></a>例
 ここに、ユーザーが入力するテキストの行を示します。 行の下の数字は、パーサが行内のその位置でどのステップをとったかを示します(解析が左から右に移動すると仮定します)。 ここで想定しているのは、"testfunc" メソッド シグネチャを含め、行の前のすべてがメソッド シグネチャ用に既に解析されているということです。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 パーサーが実行する手順を以下に示します。

1. パーサーは"testfunc"というテキストで呼び出<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>します。

2. パーサーは<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>を呼び出します。

3. パーサーは<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>を呼び出します。

4. パーサーは<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>を呼び出します。
