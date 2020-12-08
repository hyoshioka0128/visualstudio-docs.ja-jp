---
title: レガシ言語の実装 Service2 |Microsoft Docs
description: Managed package framework (MPF) を使用して、拡張言語サービス機能をサポートする従来の言語サービスを実装する方法について説明します。 第2部。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1a7da218a9ada593731e6205e017861084e73adc
ms.sourcegitcommit: 2f964946d7044cc7d49b3fc10b413ca06cb2d11b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761141"
---
# <a name="implementing-a-legacy-language-service-2"></a>従来の言語サービスの実装2
Managed package framework (MPF) を使用して言語サービスを実装するには、クラスからクラスを派生させ、 <xref:Microsoft.VisualStudio.Package.LanguageService> 次の抽象メソッドとプロパティを実装する必要があります。

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> プロパティ

  これらのメソッドとプロパティの実装の詳細については、以下の該当するセクションを参照してください。

  その他の機能をサポートするために、言語サービスでは、いずれかの MPF 言語サービスクラスからクラスを派生させる必要がある場合があります。たとえば、追加のメニューコマンドをサポートするには、クラスからクラスを派生させ、 <xref:Microsoft.VisualStudio.Package.ViewFilter> いくつかのコマンド処理メソッドをオーバーライドする必要があります (詳細については、「」を参照してください <xref:Microsoft.VisualStudio.Package.ViewFilter> )。 クラスには、 <xref:Microsoft.VisualStudio.Package.LanguageService> さまざまなクラスの新しいインスタンスを作成するために呼び出されるいくつかのメソッドが用意されています。また、クラスのインスタンスを提供する適切な作成方法をオーバーライドします。 たとえば、クラスのメソッドをオーバーライドして、 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 独自のクラスのインスタンスを返す必要があり <xref:Microsoft.VisualStudio.Package.ViewFilter> ます。 詳細については、「カスタムクラスのインスタンス化」セクションを参照してください。

  言語サービスでは、さまざまな場所で使用される独自のアイコンを指定することもできます。 たとえば、IntelliSense の入力候補一覧が表示されている場合、リスト内の各項目は、関連付けられているアイコンを持つことができます。また、項目をメソッド、クラス、名前空間、プロパティ、または任意の言語に対して必要なものとしてマークできます。 これらのアイコンは、すべての IntelliSense リスト、 **ナビゲーションバー**、および **エラー一覧** タスクウィンドウで使用されます。 詳細については、後述の「言語サービスイメージ」セクションを参照してください。

## <a name="getlanguagepreferences-method"></a>Get言語設定メソッド
 メソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 常に同じクラスのインスタンスを返し <xref:Microsoft.VisualStudio.Package.LanguagePreferences> ます。 <xref:Microsoft.VisualStudio.Package.LanguagePreferences>言語サービスに対して追加の設定が不要な場合は、基本クラスを使用できます。 MPF 言語サービスクラスは、少なくとも基本クラスが存在することを前提として <xref:Microsoft.VisualStudio.Package.LanguagePreferences> います。

### <a name="example"></a>例
 この例は、メソッドの一般的な実装を示して <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> います。 この例では、基本クラスを使用 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(TestLanguageService).GUID,
                                                        this.Name );
                m_preferences.Init();
            }
            return m_preferences;
        }
    }
}
```

## <a name="getscanner-method"></a>GetScanner メソッド
 このメソッド <xref:Microsoft.VisualStudio.Package.IScanner> は、トークンとその型およびトリガーを取得するために使用されるライン指向パーサーまたはスキャナーを実装するオブジェクトのインスタンスを返します。 このスキャナーは、色付けのためにクラスで使用され <xref:Microsoft.VisualStudio.Package.Colorizer> ます。ただし、より複雑な解析操作に準備としてトークンの種類とトリガーを取得するためにスキャナーを使用することもできます。 インターフェイスを実装するクラスを指定する必要があり <xref:Microsoft.VisualStudio.Package.IScanner> ます。また、インターフェイスにすべてのメソッドを実装する必要があり <xref:Microsoft.VisualStudio.Package.IScanner> ます。

### <a name="example"></a>例
 この例は、メソッドの一般的な実装を示して <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> います。 `TestScanner`クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.Package.IScanner> ます (表示されません)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private TestScanner m_scanner;

        public override IScanner GetScanner(IVsTextLines buffer)
        {
            if (m_scanner == null)
            {
                m_scanner = new TestScanner(buffer);
            }
            return m_scanner;
        }
    }
}
    internal class TestScanner : IScanner
    {
        private IVsTextBuffer m_buffer;
        string m_source;

        public TestScanner(IVsTextBuffer buffer)
        {
            m_buffer = buffer;
        }

        bool IScanner.ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo, ref int state)
        {
            tokenInfo.Type = TokenType.Unknown;
            tokenInfo.Color = TokenColor.Text;
            return true;
        }

        void IScanner.SetSource(string source, int offset)
        {
            m_source = source.Substring(offset);
        }
    }

```

## <a name="parsesource-method"></a>ParseSource メソッド
 さまざまな理由に基づいてソースファイルを解析します。 このメソッドには、 <xref:Microsoft.VisualStudio.Package.ParseRequest> 特定の解析操作で想定されるものを記述するオブジェクトが与えられます。 メソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> トークンの機能とスコープを決定するより複雑なパーサーを呼び出します。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドは、IntelliSense 操作のサポートと、中かっこの照合に使用されます。 このような高度な操作をサポートしていない場合でも、有効なオブジェクトを返す必要があり <xref:Microsoft.VisualStudio.Package.AuthoringScope> ます。また、インターフェイスを実装するクラスを作成 <xref:Microsoft.VisualStudio.Package.AuthoringScope> し、そのインターフェイスにすべてのメソッドを実装する必要があります。 すべてのメソッドから null 値を返すことができますが、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクト自体を null 値にすることはできません。

### <a name="example"></a>例
 この例では、メソッドとクラスの最小限の実装を示し <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> て <xref:Microsoft.VisualStudio.Package.AuthoringScope> います。これにより、言語サービスをコンパイルして、より高度な機能を実際にサポートせずに機能させることができます。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            return new TestAuthoringScope();
        }
    }

    internal class TestAuthoringScope : AuthoringScope
    {
        public override string GetDataTipText(int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return null;
        }

        public override string Goto(VSConstants.VSStd97CmdID cmd, IVsTextView textView, int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Methods GetMethods(int line, int col, string name)
        {
            return null;
        }
}
```

## <a name="name-property"></a>Name プロパティ
 このプロパティは、言語サービスの名前を返します。 これは、言語サービスの登録時に指定した名前と同じである必要があります。 この名前は、さまざまな場所で使用されます。最も目立つのは、その <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 名前がレジストリへのアクセスに使用されるクラスです。 このプロパティによって返される名前は、レジストリエントリとキー名のレジストリで使用されるので、ローカライズしないでください。

### <a name="example"></a>例
 この例は、プロパティの考えられる1つの実装を示して <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> います。 ここでの名前はハードコーディングされていることに注意してください。実際の名前は、言語サービスの登録に使用できるように、リソースファイルから取得する必要があります (「 [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override string Name
        {
            get { return "Test Language"; }
        }
    }
}
```

## <a name="instantiating-custom-classes"></a>カスタムクラスのインスタンス化
 指定されたクラスの次のメソッドは、各クラスの独自のバージョンのインスタンスを提供するようにオーバーライドできます。

### <a name="in-the-languageservice-class"></a>LanguageService クラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|テキストビューへのカスタム追加をサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|カスタムドキュメントプロパティをサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|**ナビゲーションバー** をサポートする場合は。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|コードスニペットテンプレート内の関数をサポートする場合は。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|コードスニペットをサポートする場合は。通常、このメソッドはオーバーライドされません。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|構造体のカスタマイズをサポートする <xref:Microsoft.VisualStudio.Package.ParseRequest> 場合は。通常、このメソッドはオーバーライドされません。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|ソースコードの書式設定、コメント文字の指定、およびメソッドシグネチャのカスタマイズをサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|追加のメニューコマンドをサポートする場合は。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|構文の強調表示をサポートする場合は。通常、このメソッドはオーバーライドされません。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|言語設定へのアクセスをサポートします。 このメソッドは実装する必要がありますが、基底クラスのインスタンスを返すことができます。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|行のトークンの種類を識別するために使用されるパーサーを提供します。 このメソッドは実装する必要があり、 <xref:Microsoft.VisualStudio.Package.IScanner> から派生する必要があります。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|ソースファイル全体を通じて機能とスコープを識別するために使用されるパーサーを提供します。 このメソッドは実装する必要があり、クラスのバージョンのインスタンスを返す必要があり <xref:Microsoft.VisualStudio.Package.AuthoringScope> ます。 サポートするすべてのが、メソッドから返されたパーサーを必要とする構文の強調表示である場合は、メソッドが <xref:Microsoft.VisualStudio.Package.IScanner> <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> すべて null 値を返すクラスのバージョンを返す以外に、このメソッドで何も実行できません。|

### <a name="in-the-source-class"></a>ソースクラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|IntelliSense 入力候補一覧の表示をカスタマイズする場合 (通常はオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|エラー一覧タスク一覧のマーカーをサポートするには、具体的には、ファイルを開いてエラーの原因となった行にジャンプする以外にも機能がサポートされます。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|IntelliSense パラメーターヒントの表示をカスタマイズするために使用します。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|コメントコードをサポートします。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|解析操作中に情報を収集します。|

### <a name="in-the-authoringscope-class"></a>AuthoringScope クラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|メンバーや型などの宣言の一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、オブジェクトはクラスのインスタンスである必要があり <xref:Microsoft.VisualStudio.Package.Declarations> ます。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|指定されたコンテキストのメソッドシグネチャの一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、オブジェクトはクラスのインスタンスである必要があり <xref:Microsoft.VisualStudio.Package.Methods> ます。|

## <a name="language-service-images"></a>言語サービスのイメージ
 言語サービス全体で使用されるアイコンの一覧を指定するには、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> クラスのメソッドをオーバーライド <xref:Microsoft.VisualStudio.Package.LanguageService> し、 <xref:System.Windows.Forms.ImageList> アイコンを含むを返します。 基本クラスは、 <xref:Microsoft.VisualStudio.Package.LanguageService> アイコンの既定のセットを読み込みます。 アイコンが必要な場所に正確なイメージインデックスを指定するので、独自のイメージリストをどのように配置するかは、ユーザーによって異なります。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense 入力候補一覧で使用されるイメージ
 IntelliSense 入力候補一覧の場合、イメージインデックスは、クラスのメソッドの各項目に対して指定され <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> <xref:Microsoft.VisualStudio.Package.Declarations> ます。イメージインデックスを指定する場合は、これをオーバーライドする必要があります。 メソッドから返される値 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> は、クラスコンストラクターに指定されたイメージリストのインデックスであり、クラスの <xref:Microsoft.VisualStudio.Package.CompletionSet> メソッドから返されるイメージリストと同じです <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> (クラスのメソッドをオーバーライドして別の <xref:Microsoft.VisualStudio.Package.LanguageService> イメージリストを指定する場合は、に使用するイメージリストを変更でき <xref:Microsoft.VisualStudio.Package.CompletionSet> <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> <xref:Microsoft.VisualStudio.Package.Source> ます)。

### <a name="images-used-in-the-navigation-bar"></a>ナビゲーションバーで使用されるイメージ
 **ナビゲーションバー** には、型とメンバーの一覧が表示されます。クイックナビゲーションでは、アイコンを表示できます。 これらのアイコンはクラスのメソッドから取得され、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> **ナビゲーションバー** 専用にオーバーライドすることはできません。 コンボボックス内の各項目に使用されるインデックスは、コンボボックスを表すリストがクラスのメソッドに入力されるときに指定され <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> ます (「 [従来の言語サービスでのナビゲーションバーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)」を参照してください)。 これらのイメージのインデックスは、通常はバージョンのクラスを使用してパーサーから取得され <xref:Microsoft.VisualStudio.Package.Declarations> ます。 インデックスがどのように取得されるかは、ユーザーによって異なります。

### <a name="images-used-in-the-error-list-task-window"></a>[エラー一覧タスク] ウィンドウで使用されるイメージ
 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドパーサー ([従来の言語サービスパーサーとスキャナーを](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)参照) がエラーを検出し、そのエラーをクラスのメソッドに渡すたびに、[ <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> **エラー一覧** タスク] ウィンドウにエラーが報告されます。 アイコンは、タスクウィンドウに表示される各項目に関連付けることができ、そのアイコンは、クラスのメソッドから返されたものと同じイメージリストから取得され <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。 MPF クラスの既定の動作では、エラーメッセージと共に画像が表示されません。 ただし、クラスからクラスを派生させ、メソッドをオーバーライドすることによって、この動作をオーバーライドでき <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> ます。 このメソッドでは、新しいオブジェクトを作成し <xref:Microsoft.VisualStudio.Package.DocumentTask> ます。 オブジェクトを返す前に、オブジェクトのプロパティを使用して <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> <xref:Microsoft.VisualStudio.Package.DocumentTask> イメージのインデックスを設定できます。 これは、次の例のようになります。 `TestIconImageIndex`は、すべてのアイコンを一覧表示し、この例に固有の列挙体です。 言語サービスでアイコンを識別する方法が異なる場合があります。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestSource : Source
    {
        public override DocumentTask CreateErrorTaskItem(
            TextSpan          span,
            string            filename,
            string            message,
            TaskPriority      priority,
            TaskCategory      category,
            MARKERTYPE        markerType,
            TaskErrorCategory errorCategory)
        {
            DocumentTask taskItem = base.CreateErrorTaskItem(
                                           span,
                                           filename,
                                           message,
                                           priority,
                                           category,
                                           markerType,
                                           errorCategory);
            if (errorCategory == TaskErrorCategory.Error)
            {
                taskItem.ImageIndex = TestIconImageIndex.Error;
            }
            return taskItem;
        }
    }
}
```

## <a name="the-default-image-list-for-a-language-service"></a>言語サービスの既定のイメージリスト
 基本 MPF 言語サービスクラスに用意されている既定のイメージリストには、より一般的な言語要素に関連付けられている多数のアイコンが含まれています。 これらのアイコンの多くは、パブリック、内部、友人、保護、プライベート、およびショートカットのアクセス概念に対応する6つのバリエーションのセットにまとめられています。 たとえば、メソッドがパブリック、保護、プライベートのいずれであるかに応じて、異なるアイコンを使用できます。

 次の列挙体では、各アイコンセットの一般的な名前を指定し、関連付けられているインデックスを指定します。 たとえば、列挙体に基づいて、保護されたメソッドのイメージインデックスをとして指定でき `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected` ます。 この列挙体の名前は、必要に応じて変更できます。

```csharp
public enum IconImageIndex
        {
            // access types
            AccessPublic = 0,
            AccessInternal = 1,
            AccessFriend = 2,
            AccessProtected = 3,
            AccessPrivate = 4,
            AccessShortcut = 5,

            Base = 6,
            // Each of the following icon type has 6 versions,
            //corresponding to the access types
            Class = Base + 0,
            Constant = Base + 1,
            Delegate = Base + 2,
            Enumeration = Base + 3,
            EnumMember = Base + 4,
            Event = Base + 5,
            Exception = Base + 6,
            Field = Base + 7,
            Interface = Base + 8,
            Macro = Base + 9,
            Map = Base + 10,
            MapItem = Base + 11,
            Method = Base + 12,
            OverloadedMethod = Base + 13,
            Module = Base + 14,
            Namespace = Base + 15,
            Operator = Base + 16,
            Property = Base + 17,
            Struct = Base + 18,
            Template = Base + 19,
            Typedef = Base + 20,
            Type = Base + 21,
            Union = Base + 22,
            Variable = Base + 23,
            ValueType = Base + 24,
            Intrinsic = Base + 25,
            JavaMethod = Base + 26,
            JavaField = Base + 27,
            JavaClass = Base + 28,
            JavaNamespace = Base + 29,
            JavaInterface = Base + 30,
            // Miscellaneous icons with one icon for each type.
            Error = 187,
            GreyedClass = 188,
            GreyedPrivateMethod = 189,
            GreyedProtectedMethod = 190,
            GreyedPublicMethod = 191,
            BrowseResourceFile = 192,
            Reference = 193,
            Library = 194,
            VBProject = 195,
            VBWebProject = 196,
            CSProject = 197,
            CSWebProject = 198,
            VB6Project = 199,
            CPlusProject = 200,
            Form = 201,
            OpenFolder = 202,
            ClosedFolder = 203,
            Arrow = 204,
            CSClass = 205,
            Snippet = 206,
            Keyword = 207,
            Info = 208,
            CallBrowserCall = 209,
            CallBrowserCallRecursive = 210,
            XMLEditor = 211,
            VJProject = 212,
            VJClass = 213,
            ForwardedType = 214,
            CallsTo = 215,
            CallsFrom = 216,
            Warning = 217,
        }
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
