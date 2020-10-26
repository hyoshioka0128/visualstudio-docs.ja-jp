---
title: 'チュートリアル: コアエディターの作成とエディターファイルの種類の登録 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - walkthrough
ms.assetid: 24d2bffd-a35c-46db-8515-fd60b884b7fb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 14296aa335ba6710d4d9eac8e5338af7463c0aac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687636"
---
# <a name="walkthrough-creating-a-core-editor-and-registering-an-editor-file-type"></a>チュートリアル: コア エディターの作成とエディター ファイルの種類の登録
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] myext ファイル名拡張子を持つファイルが読み込まれたときに、コアエディターを起動する VSPackage を作成する方法について説明します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio パッケージプロジェクトテンプレートの場所  
 Visual Studio パッケージのプロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログの次の 3 つの場所にあります。  
  
1. Visual Basic の機能拡張の下。 プロジェクトの既定の言語は Visual Basic です。  
  
2. C# の機能拡張の下。 プロジェクトの既定の言語は C# です。  
  
3. その他のプロジェクトの種類の機能拡張の下。 プロジェクトの既定の言語は C++ です。  
  
### <a name="to-create-the-vspackage"></a>VSPackage を作成するには  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [!INCLUDE[csprcs](../includes/csprcs-md.md)] `MyPackage` 「[チュートリアル: メニューコマンドの作成 VSPackage](https://msdn.microsoft.com/d699c149-5d1e-47ff-94c7-e1222af02c32)」に記載されているように、を起動し、という名前の VSPackage を作成します。  
  
### <a name="to-add-the-editor-factory"></a>エディターファクトリを追加するには  
  
1. **MyPackage**プロジェクトを右クリックし、[**追加**] をポイントして、[**クラス**] をクリックします。  
  
2. [ **新しい項目の追加** ] ダイアログボックスで、[ **クラス** テンプレート] が選択されていることを確認し、名前として「」と入力し、 `EditorFactory.cs` [ **追加** ] をクリックしてクラスをプロジェクトに追加します。  
  
     EditorFactory.cs ファイルを自動的に開く必要があります。  
  
3. コードから次のアセンブリを参照します。  
  
    ```vb  
    Imports System.Runtime.InteropServices  
    Imports Microsoft.VisualStudio  
    Imports Microsoft.VisualStudio.Shell  
    Imports Microsoft.VisualStudio.Shell.Interop  
    Imports Microsoft.VisualStudio.OLE.Interop  
    Imports Microsoft.VisualStudio.TextManager.Interop  
    Imports IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider  
    ```  
  
    ```csharp  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio.TextManager.Interop;  
    using IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider;  
  
    ```  
  
4. クラス宣言の直前に `EditorFactory` 属性を追加して、クラスに GUID を追加し `Guid` ます。  
  
     新しい GUID を生成するには、コマンドプロンプトで guidgen.exe プログラムを使用する [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] か、[**ツール**] メニューの [ **GUID の作成**] をクリックします。 ここで使用されている GUID は一例です。プロジェクトでは使用しないでください。  
  
    ```vb  
    <Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")> _  
    ```  
  
    ```csharp  
    [Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")]   
    ```  
  
5. クラス定義で、親パッケージとサービスプロバイダーを格納するための2つのプライベート変数を追加します。  
  
    ```vb  
    Class EditorFactory  
        Private parentPackage As Package  
        Private serviceProvider As IOleServiceProvider  
    ```  
  
    ```csharp  
    class EditorFactory  
    {  
        private Package parentPackage;  
        private IOleServiceProvider serviceProvider;  
    }  
  
    ```  
  
6. 型の1つのパラメーターを受け取るパブリッククラスコンストラクターを追加し <xref:Microsoft.VisualStudio.Shell.Package> ます。  
  
    ```vb  
    Public Sub New(ByVal parentPackage As Package)  
        Me.parentPackage = parentPackage  
    End Sub  
    ```  
  
    ```csharp  
    public EditorFactory(Package parentPackage)  
    {  
        this.parentPackage = parentPackage;  
    }  
    ```  
  
7. `EditorFactory`インターフェイスから派生するようにクラス宣言を変更し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。  
  
    ```vb  
    Class EditorFactory Implements IVsEditorFacto  
    ```  
  
    ```csharp  
    class EditorFactory : IVsEditorFactory  
  
    ```  
  
8. を右クリックし <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 、[ **インターフェイスの実装**] をクリックして、[インターフェイスの **明示的な実装**] をクリックします。  
  
     これにより、インターフェイスに実装する必要がある4つのメソッドが追加され <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。  
  
9. `IVsEditorFactory.Close` メソッドの内容を次のコードに置き換えます。  
  
    ```vb  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
10. の内容を次の `IVsEditorFactory.SetSite` コードに置き換えます。  
  
    ```vb  
    Me.serviceProvider = psp  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    this.serviceProvider = psp;  
    return VSConstants.S_OK;  
    ```  
  
11. `IVsEditorFactory.MapLogicalView` メソッドの内容を次のコードに置き換えます。  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_NOTIMPL  
    pbstrPhysicalView = Nothing ' We support only one view.  
    If rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer)OrElse _  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary) Then  
        retval = VSConstants.S_OK  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_NOTIMPL;  
    pbstrPhysicalView = null;   // We support only one view.  
    if (rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer) ||  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary))  
    {  
        retval = VSConstants.S_OK;  
    }  
    return retval;  
    ```  
  
12. `IVsEditorFactory.CreateEditorInstance` メソッドの内容を次のコードに置き換えます。  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_FAIL          
  
    ' Initialize these to empty to start with   
    ppunkDocView = IntPtr.Zero  
    ppunkDocData = IntPtr.Zero  
    pbstrEditorCaption = ""  
    pguidCmdUI = Guid.Empty  
    pgrfCDW = 0  
  
    If (grfCreateDoc And (VSConstants.CEF_OPENFILE Or _  
    VSConstants.CEF_SILENT)) = 0 Then  
        Throw New ArgumentException("Only Open or Silent is valid")  
    End If  
    If punkDocDataExisting <> IntPtr.Zero Then  
        Return VSConstants.VS_E_INCOMPATIBLEDOCDATA  
    End If  
  
    ' Instantiate a text buffer of type VsTextBuffer.   
    ' Note: we only need an IUnknown (object) interface for   
    ' this invocation.   
    Dim clsidTextBuffer As Guid = GetType(VsTextBufferClass).GUID  
    Dim iidTextBuffer As Guid = VSConstants.IID_IUnknown  
    Dim pTextBuffer As Object = pTextBuffer = _  
    parentPackage.CreateInstance(clsidTextBuffer, iidTextBuffer, _  
    GetType(Object))  
  
    If Not pTextBuffer Is Nothing Then  
        ' "Site" the text buffer with the service provider we were   
        ' provided.   
        Dim textBufferSite As IObjectWithSite = TryCast(pTextBuffer, _  
        IObjectWithSite)  
        If Not textBufferSite Is Nothing Then  
            textBufferSite.SetSite(Me.serviceProvider)  
        End If  
  
        ' Instantiate a code window of type IVsCodeWindow.   
        Dim clsidCodeWindow As Guid = GetType(VsCodeWindowClass).GUID  
        Dim iidCodeWindow As Guid = GetType(IVsCodeWindow).GUID  
        Dim pCodeWindow As IVsCodeWindow = _  
        CType(Me.parentPackage.CreateInstance(clsidCodeWindow, _  
        iidCodeWindow, GetType(IVsCodeWindow)), IVsCodeWindow)  
        If Not pCodeWindow Is Nothing Then  
            ' Give the text buffer to the code window.   
            ' We are giving up ownership of the text buffer!   
            pCodeWindow.SetBuffer(CType(pTextBuffer, IVsTextLines))  
  
            ' Now tell the caller about all this new stuff   
            ' that has been created.   
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow)  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer)  
  
            ' Specify the command UI to use so keypresses are   
            ' automatically dealt with.   
            pguidCmdUI = VSConstants.GUID_TextEditorFactory  
  
            ' This caption is appended to the filename and   
            ' lets us know our invocation of the core editor   
            ' is up and running.   
            pbstrEditorCaption = " [MyPackage]"  
  
            retval = VSConstants.S_OK  
        End If  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_FAIL;  
  
    // Initialize these to empty to start with  
    ppunkDocView       = IntPtr.Zero;  
    ppunkDocData       = IntPtr.Zero;  
    pbstrEditorCaption = "";  
    pguidCmdUI         = Guid.Empty;   
    pgrfCDW            = 0;  
  
    if ((grfCreateDoc & (VSConstants.CEF_OPENFILE |   
          VSConstants.CEF_SILENT)) == 0)  
    {   
        throw new ArgumentException("Only Open or Silent is valid");  
    }  
    if (punkDocDataExisting != IntPtr.Zero)  
    {  
        return VSConstants.VS_E_INCOMPATIBLEDOCDATA;  
    }  
  
    // Instantiate a text buffer of type VsTextBuffer.  
    // Note: we only need an IUnknown (object) interface for   
    // this invocation.  
    Guid clsidTextBuffer = typeof(VsTextBufferClass).GUID;  
    Guid iidTextBuffer   = VSConstants.IID_IUnknown;  
    object pTextBuffer   = pTextBuffer = parentPackage.CreateInstance(  
          ref clsidTextBuffer,  
          ref iidTextBuffer,  
          typeof(object));  
  
    if (pTextBuffer != null)  
    {  
        // "Site" the text buffer with the service provider we were  
        // provided.  
        IObjectWithSite textBufferSite = pTextBuffer as IObjectWithSite;  
        if (textBufferSite != null)  
        {  
            textBufferSite.SetSite(this.serviceProvider);  
        }  
  
        // Instantiate a code window of type IVsCodeWindow.  
        Guid clsidCodeWindow = typeof(VsCodeWindowClass).GUID;  
        Guid iidCodeWindow   = typeof(IVsCodeWindow).GUID;  
        IVsCodeWindow pCodeWindow =  
        (IVsCodeWindow)this.parentPackage.CreateInstance(   
              ref clsidCodeWindow,  
              ref iidCodeWindow,  
              typeof(IVsCodeWindow));  
        if (pCodeWindow != null)  
        {  
            // Give the text buffer to the code window.  
            // We are giving up ownership of the text buffer!  
            pCodeWindow.SetBuffer((IVsTextLines)pTextBuffer);  
  
            // Now tell the caller about all this new stuff   
            // that has been created.  
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow);  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer);  
  
            // Specify the command UI to use so keypresses are   
            // automatically dealt with.  
            pguidCmdUI = VSConstants.GUID_TextEditorFactory;  
  
            // This caption is appended to the filename and  
            // lets us know our invocation of the core editor   
            // is up and running.  
            pbstrEditorCaption = " [MyPackage]";  
  
            retval = VSConstants.S_OK;  
        }   
    }   
    return retval;   
    ```  
  
13. プロジェクトをコンパイルし、エラーがないことを確認します。  
  
### <a name="to-register-the-editor-factory"></a>エディターファクトリを登録するには  
  
1. **ソリューションエクスプローラー**で、リソースの .resx ファイルをダブルクリックして、文字列テーブルに開きます。このファイルは、 **String1**というエントリが選択されています。  
  
2. 識別子の名前をに変更 `IDS_EDITORNAME` し、テキストを**MyPackage エディター**に変更します。 この文字列は、エディターの名前として表示されます。  
  
3. VSPackage ファイルを開き、新しい文字列を追加します。名前を **101** に設定し、値をに設定し `IDS_EDITORNAME` ます。 これにより、パッケージには、作成した文字列にアクセスするためのリソース ID が提供されます。  
  
    > [!NOTE]
    > VSPackage ファイルに、属性が101に設定された別の文字列が含まれている場合は、 `name` 次の手順で別の一意の数値を指定します。 **101**  
  
4. **ソリューションエクスプローラー**で、MyPackagePackage.cs ファイルを開きます。  
  
     これはメインパッケージファイルです。  
  
5. 属性の直前に、次のユーザー属性を追加し `Guid` ます。  
  
    ```vb  
    <ProvideEditorFactoryAttribute(GetType(EditorFactory), 101)> _  
    <ProvideEditorExtensionAttribute(GetType(EditorFactory), _  
          ".myext", 32, NameResourceID:=101 )> _  
    ```  
  
    ```csharp  
    [ProvideEditorFactory(typeof(EditorFactory), 101)]  
    [ProvideEditorExtension(typeof(EditorFactory),   
          ".myext", 32, NameResourceID = 101)]   
    ```  
  
     属性は、この <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute> 拡張子を持つファイルが読み込まれるたびにエディターファクトリが呼び出されるように、myext ファイル拡張子とエディターファクトリを関連付けます。  
  
6. コンストラクターの直前にプライベート変数をクラスに追加 `MyPackage` し、型を指定し `EditorFactory` ます。  
  
    ```vb  
    Private editorFactory As EditorFactory  
    ```  
  
    ```csharp  
    private EditorFactory editorFactory;  
    ```  
  
7. メソッドを見つけ `Initialize` ます (非表示の領域を開いて、の `Package Members` 呼び出しの後に次のコードを追加することが必要になる場合があり `base.Initialize()` ます)。  
  
    ```vb  
    'Create our editor factory and register it.   
    Me.editorFactory = New EditorFactory(Me)  
    MyBase.RegisterEditorFactory(Me.editorFactory)  
    ```  
  
    ```csharp  
    // Create our editor factory and register it.  
    this.editorFactory = new EditorFactory(this);  
    base.RegisterEditorFactory(this.editorFactory);  
  
    ```  
  
8. プログラムをコンパイルして、エラーがないかどうかを確認します。  
  
     この手順では、の実験用レジストリハイブにエディターファクトリを登録 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] します。 Resource.h ファイルを上書きするかどうかを確認するメッセージが表示されたら、[ **OK]** をクリックします。  
  
9. Textfile1.txt という名前のサンプルファイルを作成します。  
  
10. **F5**キーを押して、実験的なインスタンスを開き [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
11. 試験段階で、[ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **ファイル** ] メニューの [ **開く** ] をポイントし、[ **ファイル**] をクリックします。  
  
12. Textfile1.txt を見つけて、[ **開く**] をクリックします。  
  
     これでファイルが読み込まれます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コアエディターは、さまざまなテキストベースのファイルの種類を処理し、言語サービスと密接に連携して、構文の強調表示、かっこの一致、IntelliSense の単語入力候補、メンバー入力候補一覧などの豊富な機能セットを提供します。 テキストベースのファイルを操作している場合は、特定のファイルの種類をサポートするカスタム言語サービスと共に、コアエディターを使用できます。  
  
 VSPackage は、エディターファクトリを指定することで、コアエディターを呼び出すことができ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 このエディターファクトリは、関連付けられているファイルが読み込まれるたびに使用されます。 ファイルがプロジェクトの一部である場合、VSPackage によってオーバーライドされない限り、コアエディターは自動的に呼び出されます。 ただし、ファイルがプロジェクトの外部に読み込まれる場合は、VSPackage によってコアエディターが明示的に呼び出される必要があります。  
  
 コアエディターの詳細については、「 [コアエディターの内部](../extensibility/inside-the-core-editor.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [コアエディター内](../extensibility/inside-the-core-editor.md)   
 [レガシ API を使用するコア エディターのインスタンス化](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)
