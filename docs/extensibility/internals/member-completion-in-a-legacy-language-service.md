---
title: 従来の言語サービスでのメンバーの完了 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707192"
---
# <a name="member-completion-in-a-legacy-language-service"></a>従来の言語サービスでのメンバー補完

IntelliSense メンバー補完は、クラス、構造体、列挙型、名前空間など、特定のスコープの使用可能なメンバーの一覧を表示するツールヒントです。 たとえば、C# では、ユーザーが "this" に続けてピリオドを入力すると、現在のスコープのクラスまたは構造体のすべてのメンバーのリストが、ユーザーが選択できる一覧に表示されます。

Managed package framework (MPF) では、ツールヒントをサポートし、ツールヒントの一覧を管理します。必要なのは、一覧に表示されるデータを提供するためにパーサーから協力することだけです。

従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="how-it-works"></a>動作のしくみ

MPF クラスを使用してメンバーリストを表示するには、次の2つの方法があります。

- 識別子にカレットを配置するか、メンバーの完了文字の後にカーソルを置いて、 **IntelliSense**メニューから [**メンバーの一覧表示**] を選択します。

- スキャナーは、 <xref:Microsoft.VisualStudio.Package.IScanner> メンバーの完了文字を検出し、その文字に対して [TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) のトークントリガーを設定します。

メンバーの完了文字は、クラス、構造体、または列挙体のメンバーが従うことを示します。 たとえば、C# または Visual Basic メンバーの完了文字はです `.` 。 C++ では、文字は `.` または `->` です。 トリガーの値は、メンバーの選択文字がスキャンされるときに設定されます。

### <a name="the-intellisense-member-list-command"></a>IntelliSense メンバーリストコマンド

この <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドは、クラスのメソッドへの呼び出しを開始します。 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.Source> メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> [ParseReason](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>)の解析理由でメソッドパーサーを呼び出します。

パーサーは、現在の位置のコンテキストと、現在の位置の前または直後のトークンを決定します。 このトークンに基づいて、宣言の一覧が表示されます。 たとえば、C# では、クラスメンバーにキャレットを配置し、[メンバーの **一覧**] を選択すると、クラスのすべてのメンバーの一覧が取得されます。 オブジェクト変数の後に続くピリオドの後にカレットを配置すると、そのオブジェクトが表すクラスのすべてのメンバーのリストが取得されます。 メンバーリストが表示されているときに、カレットがメンバーに配置されている場合は、一覧からメンバーを選択すると、カレットがあるメンバーがリスト内のメンバーと置き換えられます。

### <a name="the-token-trigger"></a>トークントリガー

[TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)トリガーはクラスに対してメソッドの呼び出しを開始 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> し、 <xref:Microsoft.VisualStudio.Package.Source> メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 解析の理由として[ParseReason を](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)使用してパーサーを呼び出します。 トークントリガーにも [TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>) フラグが含まれている場合、解析の理由は、メンバーの選択と中かっこの強調表示を組み合わせた [ParseReason. MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)です。

パーサーは、現在の位置のコンテキストと、メンバーの選択文字の前に入力されたものを決定します。 この情報から、パーサーによって、要求されたスコープのすべてのメンバーの一覧が作成されます。 この宣言の一覧は、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> メソッドから返されるオブジェクトに格納され <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> ます。 宣言が返されると、メンバーの完了ツールヒントが表示されます。 ツールヒントは、クラスのインスタンスによって管理され <xref:Microsoft.VisualStudio.Package.CompletionSet> ます。

## <a name="enable-support-for-member-completion"></a>メンバーの完了のサポートを有効にする

`CodeSense`IntelliSense 操作をサポートするには、レジストリエントリを1に設定する必要があります。 このレジストリエントリは、 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 言語パッケージに関連付けられている user 属性に渡される名前付きパラメーターを使用して設定できます。 言語サービスクラスは、クラスのプロパティからこのレジストリエントリの値を読み取り <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences> ます。

スキャナーから [TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)のトークントリガーが返され、パーサーが宣言の一覧を返すと、メンバーのコンプリートリストが表示されます。

## <a name="support-member-completion-in-the-scanner"></a>スキャナーのメンバーの完了をサポートする

スキャナーは、メンバーの完了文字を検出し、その文字が解析されたときに TokenTriggers のトークントリガーを設定できる必要があります[。](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)

### <a name="scanner-example"></a>スキャナーの例

メンバーの完了文字を検出し、適切なフラグを設定する簡単な例を次に示し <xref:Microsoft.VisualStudio.Package.TokenTriggers> ます。 この例は、説明を目的としたものです。 スキャナーには、 `GetNextToken` テキスト行からトークンを識別して返すメソッドが含まれていることを前提としています。 このコード例では、単純に、正しい種類の文字が表示されるたびにトリガーを設定します。

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

## <a name="support-member-completion-in-the-parser"></a>パーサーでのメンバーの完了のサポート

メンバーの完了のために、 <xref:Microsoft.VisualStudio.Package.Source> クラスはメソッドを呼び出し <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> ます。 クラスから派生したクラスにリストを実装する必要があり <xref:Microsoft.VisualStudio.Package.Declarations> ます。 実装する <xref:Microsoft.VisualStudio.Package.Declarations> 必要のあるメソッドの詳細については、クラスを参照してください。

メンバー選択文字が型指定されている場合、パーサーは [ParseReason](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>) または [ParseReason](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) を使用して呼び出されます。 オブジェクトで指定された場所 <xref:Microsoft.VisualStudio.Package.ParseRequest> は、メンバーの選択文字の直後にあります。 パーサーは、ソースコード内の特定のポイントにあるメンバーリストに表示できるすべてのメンバーの名前を収集する必要があります。 次に、パーサーは、現在の行を解析して、メンバーの選択文字に関連付けられているスコープを判断する必要があります。

このスコープは、メンバーが文字を選択する前の識別子の型に基づいています。 たとえば、C# で、型がのメンバー変数を指定する場合は、「 `languageService` `LanguageService` languageService」と入力し **ます。** クラスのすべてのメンバーの一覧を生成 `LanguageService` します。 また、C# では、これを入力 **します。** 現在のスコープ内のクラスのすべてのメンバーの一覧を生成します。

### <a name="parser-example"></a>パーサーの例

次の例は、リストを設定する方法の1つを示して <xref:Microsoft.VisualStudio.Package.Declarations> います。 このコードは、クラスのメソッドを呼び出すことによって、パーサーが宣言を作成し、リストに追加することを前提としてい `AddDeclaration` `TestAuthoringScope` ます。

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
