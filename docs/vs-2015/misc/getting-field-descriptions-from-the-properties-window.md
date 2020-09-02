---
title: '[プロパティ] ウィンドウからのフィールドの説明の取得 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Properties window, field descriptions
ms.assetid: 7d92bb6a-b9b9-4cd8-99e9-b5ee129b52a3
caps.latest.revision: 9
manager: jillfra
ms.openlocfilehash: 1d2b152fd7ed517a238f9893320bd0c36035627c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703979"
---
# <a name="getting-field-descriptions-from-the-properties-window"></a>[プロパティ] ウィンドウからのフィールドの説明の取得
**[プロパティ]** ウィンドウの下部にある説明領域に、選択したプロパティ フィールドに関連する情報が表示されます。 この機能は既定で有効になっています。 説明フィールドを非表示にするには、 **[プロパティ]** ウィンドウを右クリックし、 **[説明]** をクリックします。 これにより、メニュー ウィンドウの **[説明]** タイトルの横のチェック マークが削除されます。 同じ手順を行って **[説明]** の表示をオンに戻すことにより、フィールドを再度表示できます。  
  
 説明フィールド内の情報は <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> から取得されます。 それぞれのメソッド、インターフェイス、コクラスなどには、タイプ ライブラリのローカライズされていない `helpstring` 属性を適用できます。 [ **プロパティ** ] ウィンドウで、から文字列を取得し <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> ます。  
  
### <a name="to-specify-localized-help-strings"></a>ローカライズされたヘルプ文字列を指定するには  
  
1. タイプ ライブラリ ( `helpstringdll` ) のライブラリ ステートメントに`typelib`属性を追加します。  
  
   > [!NOTE]
   > この手順は、タイプ ライブラリがオブジェクト ライブラリ (.olb) ファイルにある場合は省略可能です。  
  
2. 文字列の `helpstringcontext` 属性を指定します。 `helpstring` 属性を指定することもできます。  
  
    これらの属性は、実際の.chm ファイルのヘルプ トピックに含まれる `helpfile` 属性と `helpcontext` 属性とは異なります。  
  
   強調表示されているプロパティ名に表示される説明情報を取得するために、[ **プロパティ** ] ウィンドウは、選択されて <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> いるプロパティに対してを呼び出し、出力文字列に必要な属性を指定し `lcid` ます。 内部的には、<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> は `helpstringdll` 属性で指定された .dll ファイルを検索し、指定されたコンテキストと `lcid` 属性を使ってその .dll ファイル上に `DLLGetDocumentation` を呼び出します。  
  
   `DLLGetDocumentation` の署名と実装は次のとおりです。  
  
```  
STDAPI DLLGetDocumentation  
(  
   ITypeLib * /* ptlib */,  
   ITypeInfo * /* ptinfo */,  
   LCID /* lcid */,  
   DWORD dwCtx,  
   BSTR * pbstrHelpString  
);  
```  
  
 `DLLGetDocumentation` 関数はDLL の .def ファイルで定義されているエクスポートである必要があります。  
  
 内部的には、実際には DLL である .olb ファイルが作成されます。 この DLL には、1 つのリソース、タイプ ライブラリ (.tlb) ファイル、および 1 つのエクスポートされた `DLLGetDocumentation`関数が含まれます。  
  
 .olb ファイルの場合は、 `helpstringdll` 属性は.tlb ファイル自体を含む同じファイルであるため省略可能です。  
  
 したがって、 **[説明]** ウィンドウに表示する文字列を取得するために最低限必要な操作は、タイプ ライブラリに `helpstring` 属性を指定することです。 これらの文字列をローカライズする場合は、 `helpstringdll` (省略可能) 属性と `helpstringcontext` (必須) 属性を指定し、 `DLLGetDocumentation`を実装する必要があります  
  
 idl の `helpstringcontext` 属性と `DLLGetDocumentation`によって取得したローカライズされた情報を取得する場合は、実装する必要のある追加のインターフェイスはありません。  
  
 別の方法でプロパティのローカライズされた名前と説明の取得には、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A> を実装します。 このメソッドの実装に関する詳細については、「 [Properties Window Fields and Interfaces](../extensibility/internals/properties-window-fields-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>   
 [プロパティウィンドウのフィールドとインターフェイス](../extensibility/internals/properties-window-fields-and-interfaces.md)   
 [プロパティの拡張](../extensibility/internals/extending-properties.md)   
 [helpstringdll](https://msdn.microsoft.com/library/121271fa-f061-492b-b87f-bbfcf4b02e7b)   
 [helpstring](https://msdn.microsoft.com/library/0401e905-a63e-4fad-98d0-d1efea111966)   
 [helpstringcontext](https://msdn.microsoft.com/library/d4cd135e-d91c-4aa3-9353-8aeb096f52cf)   
 [helpcontext](https://msdn.microsoft.com/library/6fbb022d-a4b7-4989-a02f-7f18a9b0ad96)   
 [ヘルプ](https://msdn.microsoft.com/library/d75161c1-1363-4019-ae09-e7e3b8a3971e)   
 [lcid](https://msdn.microsoft.com/library/7f248c69-ee1c-42c3-9411-39cf27c9f43d)