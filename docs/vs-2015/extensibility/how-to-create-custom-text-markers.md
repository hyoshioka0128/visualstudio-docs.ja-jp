---
title: '方法: カスタムテキストマーカーを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - custom text markers
ms.assetid: 6e32ed81-c604-4a32-9012-8db3bec7c846
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ac681879e0f7ad0902358be23d74d57ccee406f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841377"
---
# <a name="how-to-create-custom-text-markers"></a>方法: カスタム テキスト マーカーを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードを強調または整理するためのカスタムテキストマーカーを作成する場合は、次の手順を実行する必要があります。  
  
- 他のツールがアクセスできるように、新しいテキストマーカーを登録します。  
  
- テキストマーカーの既定の実装と構成を指定する  
  
- 他のプロセスがテキストマーカーを使用するために使用できるサービスを作成する  
  
  コード領域にテキストマーカーを適用する方法の詳細については、「 [方法: テキストマーカーを使用](../extensibility/how-to-use-text-markers.md)する」を参照してください。  
  
### <a name="to-register-a-custom-marker"></a>カスタムマーカーを登録するには  
  
1. 次のようにレジストリエントリを作成します。  
  
    HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio \\ *\<Version>* \ テキストエディター \ 外部マーカー\\*\<MarkerGUID>*  
  
    <em>\<MarkerGUID></em>は、 `GUID` 追加するマーカーを識別するために使用されます。  
  
    *\<Version>* はのバージョンです。たとえば、8.0 のようになります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
  
    *\<PackageGUID>* オートメーションオブジェクトを実装する VSPackage の GUID を示します。  
  
   > [!NOTE]
   > HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio のルートパスは、 \\ *\<Version>* Visual Studio シェルの初期化時に代替ルートでオーバーライドできます。詳細については、「[コマンドラインスイッチ](../extensibility/command-line-switches-visual-studio-sdk.md)」を参照してください。  
  
2. HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio、 \\ *\<Version>* テキストエディター、外部マーカーの下に4つの値を作成します。\\*\<MarkerGUID>*  
  
   - (既定)  
  
   - サービス  
  
   - DisplayName  
  
   - パッケージ  
  
   - `Default` REG_SZ 型の省略可能なエントリです。 設定すると、エントリの値は、"カスタムテキストマーカー" などの有用な識別情報を含む文字列になります。  
  
   - `Service` proffering よってカスタムテキストマーカーを提供するサービスの GUID 文字列を含む REG_SZ 型のエントリです <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider> 。 形式は {XXXXXX XXXX XXXX xxxx XXXXXXXXX} です。  
  
   - `DisplayName` カスタムテキストマーカーの名前のリソース ID を含む REG_SZ 型のエントリです。 形式は #YYYY です。  
  
   - `Package` は、サービスの `GUID` 下に一覧表示されるサービスを提供する VSPackage のを含む REG_SZ 型のエントリです。 形式は {XXXXXX XXXX XXXX xxxx XXXXXXXXX} です。  
  
### <a name="to-create-a-custom-text-marker"></a>カスタムテキストマーカーを作成するには  
  
1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> インターフェイスを実装します。  
  
     このインターフェイスの実装により、カスタムマーカー型の動作と外観が定義されます。  
  
     このインターフェイスは、  
  
    1. ユーザーが IDE を初めて起動したとき。  
  
    2. ユーザーは、IDE の [**ツール**] メニューから取得した [**オプション**] ダイアログボックスの左側のウィンドウにある [**環境**] フォルダーの [**フォントおよび色**] プロパティページで、[**既定値に戻す**] ボタンを選択します。  
  
2. メソッドの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider.GetTextMarkerType%2A> `IVsPackageDefinedTextMarkerType` 呼び出しで指定されたマーカーの種類の GUID に基づいて、どの実装を返すかを指定して、メソッドを実装します。  
  
     環境は、カスタムマーカーの種類を初めて作成するときにこのメソッドを呼び出し、カスタムマーカーの種類を識別する GUID を指定します。  
  
### <a name="to-proffer-your-marker-type-as-a-service"></a>マーカーの種類をサービスとして proffer するには  
  
1. <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager.QueryService%2A>のメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> ます。  
  
     へのポインター <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> が返されます。  
  
2. メソッドを呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.ProfferService%2A> 、カスタムマーカーの型サービスを識別する GUID を指定し、インターフェイスの実装へのポインターを提供し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ます。 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>実装では、インターフェイスの実装へのポインターを返す必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider> ます。  
  
     サービスが返されることを識別する一意のクッキー。 後でこの cookie を使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> この cookie 値を指定するインターフェイスのメソッドを呼び出すことによって、カスタムマーカーの型サービスを失効させることができます。  
  
## <a name="see-also"></a>参照  
 [レガシ API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [方法: 標準テキストマーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)   
 [方法: エラーマーカーを実装する](../extensibility/how-to-implement-error-markers.md)   
 [方法: テキスト マーカーを使用する](../extensibility/how-to-use-text-markers.md)
