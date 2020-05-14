---
title: レガシ言語サービスの実装2 |マイクロソフトドキュメント
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
ms.openlocfilehash: e435af68a893c923eafef744762c9da8505c3fb7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707676"
---
# <a name="implementing-a-legacy-language-service"></a>従来の言語サービスの実装
マネージ パッケージ フレームワーク (MPF) を使用して言語サービスを実装するには、<xref:Microsoft.VisualStudio.Package.LanguageService>クラスからクラスを派生させ、次の抽象メソッドとプロパティを実装する必要があります。

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> プロパティ

  これらのメソッドとプロパティの実装の詳細については、以下の該当するセクションを参照してください。

  追加機能をサポートするには、言語サービスで MPF 言語サービス クラスの 1 つからクラスを派生させる必要があります。たとえば、追加のメニュー コマンドをサポートするには、<xref:Microsoft.VisualStudio.Package.ViewFilter>クラスからクラスを派生させ、いくつかのコマンド処理メソッドをオーバーライドする必要があります<xref:Microsoft.VisualStudio.Package.ViewFilter>(詳細についてはを参照してください)。 この<xref:Microsoft.VisualStudio.Package.LanguageService>クラスには、さまざまなクラスの新しいインスタンスを作成するために呼び出されるメソッドが多数用意されており、クラスのインスタンスを提供するために適切な作成メソッドをオーバーライドします。 たとえば、<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラス内のメソッドをオーバーライドして、独自<xref:Microsoft.VisualStudio.Package.ViewFilter>のクラスのインスタンスを返す必要があります。 詳細については、「カスタム クラスのインスタンス化」を参照してください。

  言語サービスは、多くの場所で使用されている独自のアイコンを提供することもできます。 たとえば、IntelliSense 入力候補リストが表示されている場合、リスト内の各項目にアイコンを関連付け、その項目をメソッド、クラス、名前空間、プロパティ、または言語に必要な要素としてマークできます。 これらのアイコンは、すべての IntelliSense リスト、**ナビゲーション バー**、および **[エラー一覧**] タスク ウィンドウで使用されます。 詳細については、後述の「言語サービスイメージ」を参照してください。

## <a name="getlanguagepreferences-method"></a>メソッドを取得します。
 この<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>メソッドは、常にクラスの同<xref:Microsoft.VisualStudio.Package.LanguagePreferences>じインスタンスを返します。 言語サービスに対する<xref:Microsoft.VisualStudio.Package.LanguagePreferences>追加の設定が必要ない場合は、基本クラスを使用できます。 MPF 言語サービス クラスは、少なくとも基本<xref:Microsoft.VisualStudio.Package.LanguagePreferences>クラスの存在を前提としています。

### <a name="example"></a>例
 この例は、メソッドの一般的<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>な実装を示しています。 この例では、基本<xref:Microsoft.VisualStudio.Package.LanguagePreferences>クラスを使用します。

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

## <a name="getscanner-method"></a>スキャナーメソッドを取得します。
 このメソッドは、トークンとその型<xref:Microsoft.VisualStudio.Package.IScanner>とトリガーの取得に使用される、行指向パーサーまたはスキャナーを実装するオブジェクトのインスタンスを返します。 このスキャナーは色付け<xref:Microsoft.VisualStudio.Package.Colorizer>のためにクラスで使用されますが、スキャナーは、より複雑な解析操作の前兆としてトークンの種類とトリガーを取得するためにも使用できます。 インターフェイスを実装するクラスを<xref:Microsoft.VisualStudio.Package.IScanner>指定する必要があり、インターフェイスにすべてのメソッドを実装する<xref:Microsoft.VisualStudio.Package.IScanner>必要があります。

### <a name="example"></a>例
 この例は、メソッドの一般的<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>な実装を示しています。 この`TestScanner`クラスはインターフェイスを<xref:Microsoft.VisualStudio.Package.IScanner>実装します (図示しません)。

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

## <a name="parsesource-method"></a>メソッドを解析します。
 さまざまな理由に基づいてソース ファイルを解析します。 このメソッドには、特定<xref:Microsoft.VisualStudio.Package.ParseRequest>の解析操作で必要な処理を記述するオブジェクトが与えられます。 この<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドは、トークンの機能とスコープを決定する、より複雑なパーサーを呼び出します。 この<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドは、かっこの一致と同様に、IntelliSense 操作のサポートで使用されます。 このような高度な操作をサポートしていない場合でも、有効な<xref:Microsoft.VisualStudio.Package.AuthoringScope>オブジェクトを返す必要があり、インターフェイスを実装し、そのインターフェイス上のすべてのメソッド<xref:Microsoft.VisualStudio.Package.AuthoringScope>を実装するクラスを作成する必要があります。 すべてのメソッドから null 値を返すことができます<xref:Microsoft.VisualStudio.Package.AuthoringScope>が、オブジェクト自体が null 値であってはなりません。

### <a name="example"></a>例
 この例では、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドとクラスの最小限の実装<xref:Microsoft.VisualStudio.Package.AuthoringScope>を示しています。

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
 このプロパティは、言語サービスの名前を返します。 これは、言語サービスが登録されたときに指定された名前と同じ名前である必要があります。 この名前は、レジストリへのアクセスに使用される<xref:Microsoft.VisualStudio.Package.LanguagePreferences>クラスである場所の中で最も顕著な場所の数で使用されます。 このプロパティによって返される名前は、レジストリ エントリとキー名に使用されるローカライズしないでください。

### <a name="example"></a>例
 この例では、プロパティの実装を<xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A>1 つ示します。 ここでの名前はハードコーディングされています: 実際の名前は、言語サービスの登録に使用できるように、リソース ファイルから取得する必要があります ([レガシー言語サービスの登録を](../../extensibility/internals/registering-a-legacy-language-service1.md)参照してください)。

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

## <a name="instantiating-custom-classes"></a>カスタム クラスのインスタンス化
 指定したクラスの次のメソッドをオーバーライドして、各クラスの独自のバージョンのインスタンスを提供できます。

### <a name="in-the-languageservice-class"></a>言語サービス クラス内

|Method|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|テキスト ビューへのカスタム追加をサポートするため。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|カスタム ドキュメント プロパティをサポートするため。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|**ナビゲーション バー**をサポートするには、 をクリックします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|コード スニペット テンプレートの関数をサポートするため。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|コード スニペットをサポートするには (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|構造体のカスタマイズを<xref:Microsoft.VisualStudio.Package.ParseRequest>サポートするため (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|ソース コードの書式設定、コメント文字の指定、メソッド シグネチャのカスタマイズをサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|追加のメニュー コマンドをサポートするため。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|構文の強調表示をサポートするため (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|言語設定へのアクセスをサポートするため。 このメソッドは実装する必要がありますが、基本クラスのインスタンスを返すことができます。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|行のトークンの種類を識別するために使用するパーサーを提供します。 このメソッドは実装する必要があり<xref:Microsoft.VisualStudio.Package.IScanner>、派生する必要があります。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|ソース ファイル全体の機能とスコープを識別するために使用するパーサーを提供するため。 このメソッドは実装する必要があり、クラスのバージョンのインスタンスを<xref:Microsoft.VisualStudio.Package.AuthoringScope>返す必要があります。 サポートしたいのが構文の強調表示 (<xref:Microsoft.VisualStudio.Package.IScanner><xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>メソッドから返されるパーサーが必要) の場合、メソッドがすべて null 値を返すクラスのバージョンを<xref:Microsoft.VisualStudio.Package.AuthoringScope>返す以外に、このメソッドでは何もできません。|

### <a name="in-the-source-class"></a>ソースクラス内

|Method|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|IntelliSense コンプリート リストの表示をカスタマイズする場合 (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|エラー一覧のタスク一覧のサポート マーカー。特に、ファイルを開いてエラーの原因となった行にジャンプする以外の機能をサポートします。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|IntelliSense パラメーター情報ツールヒントの表示をカスタマイズします。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|コメント コードのサポートのため。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|解析操作中に情報を収集します。|

### <a name="in-the-authoringscope-class"></a>オーサリング スコープ クラス内

|Method|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|メンバーや型などの宣言の一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、オブジェクトは<xref:Microsoft.VisualStudio.Package.Declarations>クラスのバージョンのインスタンスである必要があります。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|特定のコンテキストのメソッド シグネチャの一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、オブジェクトは<xref:Microsoft.VisualStudio.Package.Methods>クラスのバージョンのインスタンスである必要があります。|

## <a name="language-service-images"></a>言語サービスイメージ
 言語サービス全体で使用されるアイコンのリストを提供するには、クラス内の<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>メソッドを<xref:Microsoft.VisualStudio.Package.LanguageService>オーバーライドし、アイコンを<xref:System.Windows.Forms.ImageList>含むを返します。 基本<xref:Microsoft.VisualStudio.Package.LanguageService>クラスは、既定のアイコン セットを読み込みます。 アイコンが必要な場所で正確なイメージ インデックスを指定するため、独自のイメージ リストの配置方法は完全にユーザーに任されます。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense コンプリート リストで使用されるイメージ
 IntelliSense 入力候補リストの場合、イメージ インデックスは<xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A><xref:Microsoft.VisualStudio.Package.Declarations>クラスのメソッドの各項目に対して指定されます。 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A>メソッドから返<xref:Microsoft.VisualStudio.Package.CompletionSet>される値は、クラス コンストラクターに提供されるイメージ リストのインデックスであり、<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラス内のメソッドから返されるイメージ リストと同じです (<xref:Microsoft.VisualStudio.Package.CompletionSet><xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A><xref:Microsoft.VisualStudio.Package.Source>クラス内のメソッドをオーバーライドして別のイメージ リストを提供する場合は、どのイメージ リストを使用するかを変更できます)。

### <a name="images-used-in-the-navigation-bar"></a>ナビゲーション バーで使用される画像
 **ナビゲーション バー**には、型とメンバーのリストが表示され、アイコンを表示できるクイック ナビゲーションに使用されます。 これらのアイコンは<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラスのメソッドから取得され、**ナビゲーション バー**用に特にオーバーライドすることはできません。 コンボ ボックスの各項目に使用されるインデックスは、コンボ ボックスを表すリストが<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A><xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>クラスのメソッドに入力されるときに指定されます ([従来の言語サービスのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)を参照)。 これらのイメージインデックスは、通常はクラスのバージョンを通じてパーサーから何らかの形<xref:Microsoft.VisualStudio.Package.Declarations>で取得されます。 インデックスの取得方法は、完全にあなた次第です。

### <a name="images-used-in-the-error-list-task-window"></a>エラー一覧タスク ウィンドウで使用されるイメージ
 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド パーサー ([レガシ言語サービス パーサーおよび Scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)を参照) がエラーを検出<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A>し、<xref:Microsoft.VisualStudio.Package.AuthoringSink>そのエラーをクラス内のメソッドに渡すたびに、**エラーがエラー一覧**タスク ウィンドウに報告されます。 アイコンは、タスク ウィンドウに表示される各項目に関連付けることができ、そのアイコンはクラス内の<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>メソッドから返された同じ<xref:Microsoft.VisualStudio.Package.LanguageService>イメージ リストから取得されます。 MPF クラスの既定の動作では、エラー メッセージを持つイメージを表示しません。 ただし、<xref:Microsoft.VisualStudio.Package.Source>クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>メソッドをオーバーライドすることで、この動作をオーバーライドできます。 このメソッドでは、新しい<xref:Microsoft.VisualStudio.Package.DocumentTask>オブジェクトを作成します。 オブジェクトを返す前に、オブジェクトの<xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A>プロパティを<xref:Microsoft.VisualStudio.Package.DocumentTask>使用してイメージ インデックスを設定できます。 これは次の例のようになります。 これは`TestIconImageIndex`、すべてのアイコンを一覧表示する列挙であり、この例に固有の列挙体であることに注意してください。 言語サービスでアイコンを識別する方法が異なる場合があります。

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

## <a name="the-default-image-list-for-a-language-service"></a>言語サービスの既定のイメージ リスト
 基本 MPF 言語サービス クラスに付属する既定のイメージ リストには、より一般的な言語要素に関連付けられたアイコンが多数含まれています。 これらのアイコンの大部分は、パブリック、内部、フレンド、プロテクト、プライベート、およびショートカットのアクセスコンセプトに対応する 6 つのバリエーションのセットで配置されます。 たとえば、メソッドがパブリック、保護、プライベートのいずれであるかによって、メソッドに対して異なるアイコンを設定できます。

 次の列挙体は、各アイコン セットの一般的な名前を指定し、関連付けられているインデックスを指定します。 たとえば、列挙型に基づいて、保護されたメソッドのイメージ インデックスを`(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected`として指定できます。 この列挙体の名前は、必要に応じて変更できます。

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
