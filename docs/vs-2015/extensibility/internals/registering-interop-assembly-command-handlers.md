---
title: 相互運用機能アセンブリの登録コマンドハンドラー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9d2822e9eef36806f5c251813925fb4244242519
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705813"
---
# <a name="registering-interop-assembly-command-handlers"></a>相互運用機能アセンブリ コマンド ハンドラーの登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 統合開発環境 (IDE) によってコマンドが適切にルーティングされるように、に登録する必要があります。  
  
 レジストリを更新するには、手動で編集するか、レジストラー (.rgs) ファイルを使用します。 詳細については、「 [Creating Registrar Scripts](https://msdn.microsoft.com/library/cbd5024b-8061-4a71-be65-7fee90374a35)」を参照してください。  
  
 マネージパッケージフレームワーク (MPF) は、クラスを通じてこの機能を提供し <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> ます。  
  
 [コマンドテーブル形式の参照](https://msdn.microsoft.com/09e9c6ef-9863-48de-9483-d45b7b7c798f) リソースは、アンマネージサテライト UI dll にあります。  
  
## <a name="command-handler-registration-of-a-vspackage"></a>VSPackage のコマンドハンドラーの登録  
 ユーザーインターフェイス (UI) ベースのコマンドのハンドラーとして機能する VSPackage には、VSPackage の後にという名前のレジストリエントリが必要です `GUID` 。 このレジストリエントリは、VSPackage の UI リソースファイルとそのファイル内の menu リソースの場所を指定します。 レジストリエントリ自体は HKEY_LOCAL_MACHINE \Software\Microsoft\VisualStudio \ メニューの下にあり \\ *\<Version>* ます。ここで、 *\<Version>* は9.0 などののバージョンです [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
> [!NOTE]
> シェルが初期化されると、HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio のルートパスを \\ *\<Version>* 代替ルートでオーバーライドでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 ルートパスの詳細については、「 [Windows インストーラーを使用した Vspackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。  
  
### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU リソースレジストリエントリ  
 レジストリエントリの構造は次のとおりです。  
  
```  
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\  
  Menus\  
    <GUID> = <Resource Information>  
```  
  
 \<*GUID*> は、 `GUID` {VSPackage} という形式の、XXXXXXXXX の形式です。  
  
 *\<Resource Information>* コンマで区切られた3つの要素で構成されます。 これらの要素の順序は次のとおりです。  
  
 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>  
  
 次の表では、のフィールドについて説明し \<*Resource Information*> ます。  
  
|要素|説明|  
|-------------|-----------------|  
|\<*Path to Resource DLL*>|これは、メニューリソースを含むリソース DLL への完全なパスです。これは、VSPackage のリソース DLL が使用されることを示します。これは、VSPackage 自体が登録されている Packages サブキーで指定されています。<br /><br /> 慣例として、このフィールドは空白にしておきます。|  
|\<*Menu Resource ID*>|これは、 `CTMENU` VSPackage ファイルからコンパイルされた、すべての UI 要素を含むリソースのリソース ID[です。](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|  
|\<*Menu Version*>|これは、リソースのバージョンとして使用される番号です `CTMENU` 。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、この値を使用して、リソースの内容を `CTMENU` すべてのリソースのキャッシュと再マージする必要があるかどうかを判断し `CTMENU` ます。 Devenv のセットアップコマンドを実行すると、再マージがトリガーされます。<br /><br /> この値は、最初に1に設定し、リソースのすべての変更の後、再 `CTMENU` マージが発生する前にインクリメントする必要があります。|  
  
### <a name="example"></a>例  
 いくつかのリソースエントリの例を次に示します。  
  
```  
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\  
  Menus\  
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10  
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3  
```  
  
## <a name="see-also"></a>参照  
 [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)
