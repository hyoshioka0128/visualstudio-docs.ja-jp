---
title: カスタムカテゴリの実装と項目の表示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- font and color control [Visual Studio SDK], categories
- custom categories
ms.assetid: 99311a93-d642-4344-bbf9-ff6e7fa5bf7f
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 474d5c66507b56bea609568b6acfe9f5eff75e9c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841605"
---
# <a name="implementing-custom-categories-and-display-items"></a>カスタム カテゴリと表示項目の実装
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] カスタムカテゴリと表示項目を使用して、統合開発環境 (IDE) にテキストのフォントと色を制御できます。  
  
 カスタムカテゴリと表示項目は、[ **フォントおよび色** ] プロパティページにあります。 [ **フォントおよび色** ] プロパティページを開くには、[ **ツール** ] メニューの [ **オプション**] をクリックします。 [ **環境** ] を展開し、[ **フォントおよび色**] をクリックします。  
  
 このメカニズムを使用する場合、Vspackage は <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> インターフェイスとそれに関連付けられたインターフェイスを実装する必要があります。  
  
 原則として、このメカニズムを使用して、既存のすべての **表示項目** とそれらを含む **カテゴリ** を変更できます。 ただし、 **Text EditorCategory** またはその **表示項目**の変更には使用しないでください。 詳細については、「 [フォントと色の概要](../extensibility/font-and-color-overview.md)」を参照してください。  
  
 カスタム **カテゴリ** または **表示項目**を実装するには、VSPackage が次の条件を満たす必要があります。  
  
- レジストリでカテゴリを作成または識別します。  
  
   IDE の [ **フォントおよび色** ] プロパティページの実装では、この情報を使用して、特定のカテゴリをサポートするサービスを正しく照会します。  
  
- レジストリでグループを作成または指定します (省略可能)。  
  
   2つ以上のカテゴリの和集合を表すグループを定義すると便利な場合があります。 グループが定義されている場合、IDE はサブカテゴリを自動的にマージし、グループ内の表示項目を配布します。  
  
- IDE サポートを実装します。  
  
- フォントと色の変更を処理します。  
  
  詳細については、「 [保存されたフォントと色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)」を参照してください  
  
## <a name="to-create-or-identify-categories"></a>カテゴリを作成または識別するには  
  
- [HKLM\SOFTWARE\Microsoft \\ *\<Visual Studio version>* \\ `<Category>` ] の下に特別な種類のカテゴリレジストリエントリを作成します。  
  
   *\<Category>* カテゴリのローカライズされていない名前を指定します。  
  
- 次の2つの値を使用してレジストリを設定します。  
  
  |Name|種類|Data|説明|  
  |----------|----------|----------|-----------------|  
  |カテゴリ|REG_SZ|GUID|カテゴリを識別するために作成された GUID。|  
  |パッケージ|REG_SZ|GUID|カテゴリをサポートする VSPackage サービスの GUID。|  
  
  レジストリに指定されたサービスは、対応するカテゴリのの実装を提供する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> ます。  
  
## <a name="to-create-or-identify-groups"></a>グループを作成または識別するには  
  
- [HKLM\SOFTWARE\Microsoft \\ *\<Visual Studio version>* \\ *\<group>* ] の下に特別な種類のカテゴリレジストリエントリを作成します。  
  
   *\<group>* グループのローカライズされていない名前を指定します。  
  
- 次の2つの値を使用してレジストリを設定します。  
  
  |Name|種類|Data|説明|  
  |----------|----------|----------|-----------------|  
  |カテゴリ|REG_SZ|GUID|グループを識別するために作成された GUID。|  
  |パッケージ|REG_SZ|GUID|カテゴリをサポートするサービスの GUID。|  
  
  レジストリに指定されたサービスは、対応するグループのの実装を提供する必要があり `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` ます。  
  
## <a name="to-implement-ide-support"></a>IDE サポートを実装するには  
  
- を実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider.GetObject%2A> ます。これにより、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 指定された `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` **カテゴリ** またはグループ GUID ごとに、インターフェイスまたはインターフェイスが IDE に返されます。  
  
- サポートされているすべての **カテゴリ** に対して、VSPackage はインターフェイスの個別のインスタンスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> ます。  
  
- によって実装されるメソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> IDE に次のものを提供する必要があります。  
  
  - カテゴリ内の **表示項目** の一覧 **。**  
  
  - **表示項目**のローカライズ可能な名前。  
  
  - **カテゴリ**の各メンバーの情報を表示します。  
  
  > [!NOTE]
  > すべての **カテゴリ** には、少なくとも1つの **表示項目**を含める必要があります。  
  
- IDE では、インターフェイスを使用して、 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` 複数のカテゴリの和集合を定義します。  
  
   この実装では、IDE を次のように提供します。  
  
  - 指定されたグループを構成する **カテゴリ** の一覧。  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>グループ内の各**カテゴリ**をサポートするのインスタンスへのアクセス。  
  
  - ローカライズ可能なグループ名。  
  
- IDE を更新しています:  
  
   IDE では、 **フォントおよび色** の設定に関する情報がキャッシュされます。 そのため、IDE の **フォントと色** の構成を変更した後は、キャッシュが最新の状態になっていることを確認することをお勧めします。  
  
  キャッシュの更新はインターフェイスを介して行われ、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> グローバルに、または選択した項目でのみ実行できます。  
  
## <a name="to-handle-font-and-color-changes"></a>フォントと色の変更を処理するには  
 VSPackage によって表示されるテキストの色付けを適切にサポートするには、VSPackage をサポートする色付けサービスが、[ **フォントおよび色** ] プロパティページでユーザーが開始した変更に応答する必要があります。 VSPackage は、次の方法でこれを実行します。  
  
- インターフェイスを実装することによって、IDE によって生成されたイベントを処理 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> します。  
  
     IDE は、[ **フォントおよび色** ] ページをユーザーが変更した後、適切なメソッドを呼び出します。 たとえば、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents.OnFontChanged%2A> 新しいフォントが選択されている場合は、メソッドを呼び出します。  
  
     - または -  
  
- 変更のために IDE をポーリングしています。  
  
     これは、システムによって実装されたインターフェイスを使用して行うことができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> ます。 主に永続化のサポートのために、メソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> **表示項目**のフォントと色の情報を取得できます。 詳細については、「 [格納されているフォントおよび色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)」を参照してください。  
  
    > [!NOTE]
    > ポーリングによって取得された結果が正しいことを確認するには、インターフェイスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> インターフェイスの取得メソッドを呼び出す前にキャッシュのフラッシュと更新が必要かどうかを判断し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 [テキストの色付けに関するフォントと色の情報を取得する](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [格納されているフォントと色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)   
 [方法: 組み込みフォントおよび配色にアクセスする](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)   
 [フォントと色の概要](../extensibility/font-and-color-overview.md)
