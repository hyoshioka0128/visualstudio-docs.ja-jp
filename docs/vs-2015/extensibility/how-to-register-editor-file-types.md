---
title: '方法: エディターファイルの種類を登録する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register file types
ms.assetid: 54846779-8290-48de-90ab-81011559d9a5
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8d22e61d88b5f6e3959a369f6957efbc824384b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204120"
---
# <a name="how-to-register-editor-file-types"></a>方法: エディター ファイルの種類を登録する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターファイルの種類を登録する最も簡単な方法は、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] managed package framework (MPF) クラスの一部として提供されている登録属性を使用することです。 ネイティブでパッケージを実装する場合は [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 、エディターとそれに関連付けられている拡張機能を登録するレジストリスクリプトを記述することもできます。  
  
## <a name="registration-using-mpf-classes"></a>MPF クラスを使用した登録  
  
#### <a name="to-register-editor-file-types-using-mpf-classes"></a>MPF クラスを使用してエディターファイルの種類を登録するには  
  
1. <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute>VSPackage のクラスでエディターの適切なパラメーターをクラスに提供します。  
  
    ```  
    [Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute(typeof(EditorFactory), ".Sample", 32,   
         ProjectGuid = "{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}",   
         TemplateDir = "..\\..\\Templates",   
         NameResourceID = 106)]  
    ```  
  
     Where ""サンプル" は、このエディターに登録されている拡張機能であり、"32" は優先度レベルです。  
  
     `projectGuid`は、で定義されているその他の種類のファイルの GUID です <xref:Microsoft.VisualStudio.VSConstants.CLSID.MiscellaneousFilesProject_guid> 。 その他のファイルの種類が用意されているので、作成されたファイルはビルドプロセスに含まれません。  
  
     `TemplateDir` マネージ基本エディターサンプルに含まれているテンプレートファイルを含むフォルダーを表します。  
  
     `NameResourceID` は、BasicEditorUI プロジェクトの resource.h ファイルで定義され、エディターを "My Editor" として識別します。  
  
2. <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドをオーバーライドします。  
  
     メソッドの実装で <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 、メソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> 次に示すようにエディターファクトリのインスタンスを渡します。  
  
    ```  
    protected override void Initialize()  
    {  
        Trace.WriteLine (string.Format(CultureInfo.CurrentCulture,   
        "Entering Initialize() of: {0}", this.ToString()));  
        base.Initialize();  
           //Create Editor Factory  
        editorFactory = new EditorFactory(this);  
        base.RegisterEditorFactory(editorFactory);  
    }  
    ```  
  
     この手順では、エディターファクトリとエディターの両方のファイル拡張子を登録します。  
  
3. エディターファクトリの登録を解除します。  
  
     VSPackage が破棄されると、エディターファクトリは自動的に登録解除されます。 エディターファクトリオブジェクトがインターフェイスを実装している場合 <xref:System.IDisposable> 、 `Dispose` ファクトリがで登録解除された後、そのメソッドが呼び出され [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
## <a name="registration-using-a-registry-script"></a>レジストリスクリプトを使用した登録  
 次に示すように、ネイティブでエディターファクトリとファイルの種類を登録 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] するには、レジストリスクリプトを使用して windows レジストリに書き込みます。  
  
#### <a name="to-register-editor-file-types-using-a-registry-script"></a>レジストリスクリプトを使用してエディターファイルの種類を登録するには  
  
1. レジストリスクリプトで、 `GUID_BscEditorFactory` 次のレジストリスクリプトのセクションに示すように、エディターファクトリとエディターファクトリの GUID 文字列を定義します。 また、拡張機能とエディター拡張機能の優先度を定義します。  
  
    ```  
  
          NoRemove Editors     {         %GUID_BscEditorFactory% = s 'RTF Editor'         {             val Package = s '%CLSID_Package%'             val DisplayName = s 'An RTF Editor'             val ExcludeDefTextEditor = d 1             val AcceptBinaryFiles = d 0  
  
            LogicalViews  
            {  
                val %LOGVIEWID_TextView% = s ''  
            }  
  
            OpenWithEntries  
            {  
            }  
  
            Extensions            {                val rtf = d 50            }  
        }  
    }  
    ```  
  
     この例のエディターファイルの拡張子は ".rtf" であり、その優先度は "50" です。 GUID 文字列は、BscEdit サンプルプロジェクトの resource.h ファイルで定義されています。  
  
2. VSPackage を登録します。  
  
3. エディターファクトリを登録します。  
  
     エディターファクトリは、実装に登録され <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> ます。  
  
    ```  
    // create editor factory.  
    if (m_srpEdFact == NULL)   
    {  
        CComObject<CBscEditorFactory> *pEdFact = new CComObject<CBscEditorFactory>;  
        if (NULL == pEdFact)  
          return E_OUTOFMEMORY;  
  
        if (!pEdFact->FInit(this))  
          return E_UNEXPECTED;  
  
        m_srpEdFact = (IVsEditorFactory *) pEdFact;    // Note: assignment to a smart pointer does an AddRef()  
    }  
    // Query service for IVsRegisterEditors, register the editor factory  
    CComPtr<IVsRegisterEditors> srpRegEd;  
    if ((SUCCEEDED(m_srpPkgSiteSP->QueryService(SID_SVsRegisterEditors, IID_IVsRegisterEditors,(void **)&srpRegEd ))) && (srpRegEd != NULL))  
      {  
        ATLTRACE(TEXT(">> CVsPackage, registering editor factory.\n"));  
          if (FAILED(srpRegEd->RegisterEditor(GUID_BscEditorFactory,  
                      m_srpEdFact, &m_dwEditorCookie)))   
          {  
             ATLTRACE(TEXT(">> CVsPackage, RegisterEditor() failed.\n"));  
            return E_FAIL;  
          }  
      }  
        return S_OK;  
    }  
    ```  
  
     GUID 文字列は、BscEdit プロジェクトの resource.h ファイルで定義されています。
