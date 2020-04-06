---
title: レガシー言語サービスでのメンバーの完了 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b6445aec4954590e4d361189f053592eebe7767e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707192"
---
# <a name="member-completion-in-a-legacy-language-service"></a>従来の言語サービスでのメンバー補完

IntelliSense メンバーの完了は、クラス、構造体、列挙体、または名前空間など、特定のスコープの可能なメンバーの一覧を表示するツール ヒントです。 たとえば、C# では、ユーザーが "this" の後にピリオドを入力すると、現在のスコープにあるクラスまたは構造体のすべてのメンバーのリストが、ユーザーが選択できるリストに表示されます。

管理パッケージ フレームワーク (MPF) は、ツール ヒントのサポートとツール ヒントの一覧の管理を提供します。必要なのは、リストに表示されるデータを提供するためのパーサーからの協力だけです。

レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[エディタと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="how-it-works"></a>動作のしくみ

MPF クラスを使用してメンバー・リストを表示する 2 つの方法を次に示します。

- 識別子またはメンバー入力文字の後にキャレットを配置し **、IntelliSense**メニューから **[メンバーの一覧表示**] を選択します。

- スキャナー<xref:Microsoft.VisualStudio.Package.IScanner>はメンバー完了文字を検出し、その文字のトークン[トリガーを設定します](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)。

メンバーの完了文字は、クラス、構造体、または列挙体のメンバーが従うことを示します。 たとえば、C# または Visual Basic ではメンバー入力文字`.`は a ですが、C++ では`.`メンバー入力`->`候補文字は a または a のいずれかです。 トリガー値は、メンバー選択文字がスキャンされるときに設定されます。

### <a name="the-intellisense-member-list-command"></a>インテリセンス メンバー リスト コマンド

この<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>コマンドは、クラスの<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドの呼び出<xref:Microsoft.VisualStudio.Package.Source>しを開始<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>し、メソッドは<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>[ParseReason.DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>)の解析理由を使用してメソッド パーサーを呼び出します。

パーサーは、現在の位置のコンテキストと、現在の位置の下または直前のトークンを決定します。 このトークンに基づいて、宣言のリストが表示されます。 たとえば C# では、キャレットをクラス メンバーに配置し、[**メンバの一覧**] を選択すると、そのクラスのすべてのメンバのリストが表示されます。 オブジェクト変数の後にピリオドを置くと、そのオブジェクトが表すクラスのすべてのメンバーのリストが表示されます。 メンバー・リストが表示されているときにメンバーにキャレットが配置されている場合、リストからメンバーを選択すると、キャレットがオンになっているメンバーがリスト内のメンバーに置き換えられます。

### <a name="the-token-trigger"></a>トークントリガー

トリガー[は](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)、クラスの<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドの呼び出し<xref:Microsoft.VisualStudio.Package.Source>を開始し、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドは[ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)の解析理由を使用してパーサーを呼び出します。 トークン トリガーに[TokenTriggers.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>)フラグも含まれている場合、解析の理由は、メンバーの選択と中かっこの強調表示を組み合わせた[ParseReason.MemberSelectAndHighlightBraces です](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)。

パーサーは、現在の位置のコンテキストと、メンバー選択文字の前に入力された内容を判別します。 この情報から、パーサーは要求されたスコープのすべてのメンバーのリストを作成します。 この宣言のリストは、メソッドから返<xref:Microsoft.VisualStudio.Package.AuthoringScope>されるオブジェクトに<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>格納されます。 何らかの宣言が返された場合は、メンバー完了ツール ヒントが表示されます。 ツール ヒントは、クラスのインスタンスによって管理<xref:Microsoft.VisualStudio.Package.CompletionSet>されます。

## <a name="enable-support-for-member-completion"></a>メンバーの完了のサポートを有効にする

IntelliSense`CodeSense`操作をサポートするには、レジストリ エントリを 1 に設定する必要があります。 このレジストリ エントリは、言語パッケージに関連付けられたユーザー<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性に渡される名前付きパラメータを使用して設定できます。 言語サービス クラスは、クラスのプロパティからこのレジストリ<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>エントリの値<xref:Microsoft.VisualStudio.Package.LanguagePreferences>を読み取ります。

スキャナーが[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)のトークン トリガーを返し、パーサーが宣言の一覧を返す場合は、メンバー入力候補の一覧が表示されます。

## <a name="support-member-completion-in-the-scanner"></a>スキャナーでのメンバーの補完をサポート

スキャナーは、メンバーの完了文字を検出し、その文字が解析されるときに[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)のトークン トリガーを設定できる必要があります。

### <a name="scanner-example"></a>スキャナの例

以下は、メンバー完了文字を検出し、適切な<xref:Microsoft.VisualStudio.Package.TokenTriggers>フラグを設定する簡単な例です。 この例は、説明のみを目的とします。 この例では、スキャナーに、テキスト`GetNextToken`行からトークンを識別して返すメソッドが含まれていることを前提としています。 このコード例では、適切な種類の文字が見えたときにトリガーを設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>パーサーでのメンバーの完了をサポートする

メンバーの完了に対<xref:Microsoft.VisualStudio.Package.Source>して、クラス<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>はメソッドを呼び出します。 リストは、クラスから派生したクラスで実装する<xref:Microsoft.VisualStudio.Package.Declarations>必要があります。 実装する<xref:Microsoft.VisualStudio.Package.Declarations>必要があるメソッドの詳細については、クラスを参照してください。

パーサーは、[メンバー選択](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)文字が型指定されている場合[に](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)呼び出されます。 オブジェクト内で指定された<xref:Microsoft.VisualStudio.Package.ParseRequest>位置は、メンバー選択文字の直後です。 パーサーは、ソース コード内の特定のポイントでメンバー リストに表示されるすべてのメンバーの名前を収集する必要があります。 次に、パーサーは、現在の行を解析して、ユーザーがメンバー選択文字に関連付けるスコープを決定する必要があります。

このスコープは、メンバー選択文字の前の ID のタイプに基づいています。 たとえば、C# では、型が`languageService``LanguageService`languageService の型を持つメンバー変数を指定**します。** クラスのすべてのメンバーのリストが生成されます`LanguageService`。 また、C#では、**これを入力します。** は、現在のスコープ内のクラスのすべてのメンバーのリストを生成します。

### <a name="parser-example"></a>パーサーの例

次の例は、リストを設定する<xref:Microsoft.VisualStudio.Package.Declarations>1 つの方法を示しています。 このコードは、パーサーが宣言を構築し、クラスの`AddDeclaration`メソッドを呼び出すことによってリストに追加`TestAuthoringScope`することを前提としています。

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```
