---
title: '方法: 組み込みフォントと配色にアクセスする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, accessing built-in
- font and color control [Visual Studio SDK], categories
- colors, accessing built-in schemes
ms.assetid: 6905845e-e88e-4805-adcf-21da39108ec7
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a43fb3a22ecb2d04542eacf07bf883590868b75b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685305"
---
# <a name="how-to-access-the-built-in-fonts-and-color-scheme"></a>方法: 組み込みのフォントおよび色のスキーマにアクセスする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 統合開発環境 (IDE) には、エディターウィンドウに関連付けられたフォントと色のスキームが用意されています。 このスキームには、インターフェイスを介してアクセスでき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。  
  
 組み込みのフォントおよび配色を使用するには、VSPackage で次のことを行う必要があります。  
  
- 既定のフォントおよび色サービスで使用するカテゴリを定義します。  
  
- 既定のフォントおよびカラーサーバーにカテゴリを登録します。  
  
- およびインターフェイスを使用して、特定のウィンドウが組み込みの表示項目およびカテゴリを使用することを IDE に通知し `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer` `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` ます。  
  
  IDE では、結果として得られるカテゴリがウィンドウへのハンドルとして使用されます。 カテゴリの名前は、[**フォントおよび色**] プロパティページの [**設定の表示:** ] ボックスの一覧に表示されます。  
  
### <a name="to-define-a-category-using-built-in-fonts-and-colors"></a>組み込みのフォントと色を使用してカテゴリを定義するには  
  
1. 任意の GUID を作成します。  
  
    この GUID は、カテゴリを一意に識別するために使用され<strong>ます。</strong> このカテゴリは、IDE の既定のフォントと色の指定を再利用します。  
  
   > [!NOTE]
   > またはその他のインターフェイスを使用してフォントおよびカラーデータを取得する場合 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> 、vspackage はこの GUID を使用して組み込みの情報を参照します。  
  
2. カテゴリの名前は、IDE に表示されるときに必要に応じてローカライズできるように、VSPackage のリソース (.rc) ファイル内の文字列テーブルに追加する必要があります。  
  
    詳細については、「 [文字列の追加または削除](https://msdn.microsoft.com/library/077077b4-0f4b-4633-92d6-60b321164cab)」を参照してください。  
  
### <a name="to-register-a-category-using-built-in-fonts-and-colors"></a>組み込みのフォントと色を使用してカテゴリを登録するには  
  
1. 次の場所に特別な種類のカテゴリレジストリエントリを構築します。  
  
     [HKLM\SOFTWARE\Microsoft、Visual Studio \\ *\<Visual Studio version>* \ Fontandcolors \\ *\<Category>*  
  
     *\<Category>* カテゴリのローカライズされていない名前を指定します。  
  
2. 次の4つの値で、ストックフォントと配色を使用するようにレジストリを設定します。  
  
    |名前|種類|Data|説明|  
    |----------|----------|----------|-----------------|  
    |カテゴリ|REG_SZ|GUID|ストックフォントと配色を含むカテゴリを識別する任意の GUID。|  
    |Package|REG_SZ|GUID|F5E7E71D-1401-11D1-883B-0000F87579D2<br /><br /> この GUID は、既定のフォントと色の構成を使用するすべての Vspackage によって使用されます。|  
    |NameID|REG_DWORD|id|VSPackage 内のローカライズ可能なカテゴリ名のリソース ID。|  
    |ToolWindowPackage|REG_SZ|GUID|インターフェイスを実装している VSPackage の GUID <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|  
  
3. 
  
### <a name="to-initiate-the-use-of-system-provided-fonts-and-colors"></a>システム指定のフォントと色の使用を開始するには  
  
1. `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer`ウィンドウの実装と初期化の一部として、インターフェイスのインスタンスを作成します。  
  
2. メソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` 現在のインスタンスに対応するインターフェイスのインスタンスを取得 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> します。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A>を2回呼び出します。  
  
   - を `VSEDITPROPID_ViewGeneral_ColorCategory` 引数として1回だけ呼び出します。  
  
   - を `VSEDITPROPID_ViewGeneral_FontCategory` 引数として1回だけ呼び出します。  
  
     これにより、既定のフォントおよびカラーサービスがウィンドウのプロパティとして設定され、公開されます。  
  
## <a name="example"></a>例  
 次の例では、組み込みフォントと色の使用を開始します。  
  
```  
CComVariant vt;  
CComQIPtr<IVsTextEditorPropertyCategoryContainer> spPropCatContainer(m_spView);  
if (spPropCatContainer != NULL){  
    CComPtr<IVsTextEditorPropertyContainer> spPropContainer;  
    if (SUCCEEDED(spPropCatContainer->GetPropertyCategory(GUID_EditPropCategory_View_MasterSettings,   
                                                          &spPropContainer))){  
        CComVariant vt;CComVariant VariantGUID(bstrGuidText);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_FontCategory, VariantGUID);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_ColorCategory, VariantGUID);  
    }  
}  
```  
  
## <a name="see-also"></a>参照  
 [フォントと色の使用](../extensibility/using-fonts-and-colors.md)   
 [テキストの色付けに関するフォントと色の情報を取得する](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [格納されているフォントと色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)   
 [フォントと色の概要](../extensibility/font-and-color-overview.md)
