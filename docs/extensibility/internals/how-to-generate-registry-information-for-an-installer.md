---
title: '方法: インストーラーのレジストリ情報を生成する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
- VSPackages, registration manifests
ms.assetid: b1b41012-a777-4ccf-81a6-3b41f0e96583
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b0140ea2e1b894754b0cf35bc75676f277b12a0a
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905466"
---
# <a name="how-to-generate-registry-information-for-an-installer"></a>方法: インストーラーのレジストリ情報を生成する

*RegPkg.exe*ユーティリティを使用して、マネージ VSPackage の登録マニフェストを生成できます。 マニフェストは、Windows インストーラーセットアップパッケージに組み込むことができます。 RegPkg では、 [WINDOWS インストーラー XML ツールセット](https://wixtoolset.org/)に基づいてセットアップのソースファイルに含めることができるファイルを生成することもできます。

> [!IMPORTANT]
> RegPkg では、開発システムに固有のパス名が生成されるため、RegPkg を使用するたびに、適切な Windows インストーラー書式設定されたプロパティを使用するように出力を編集する必要があります。 たとえば、値は `InprocServer32` * \<SystemFolder\>mscoree.dll*し、パスにはとを使用する必要があり *\<#filekey\>* *\<$componentkey\>* ます。 この方法で出力を調整すると、別のドライブまたは別のディレクトリに Windows がインストールされているコンピューター、ローカライズされたディレクトリ名、およびユーザーが選択できるパスがサポートされます。 詳細については、「Windows インストーラー SDK での[書式設定](https://msdn.microsoft.com/library?url=/library/msi/setup/formatted.asp)」を参照してください。 開発システムパスの RegPkg 規則 (たとえば、フォーム*File_ \<filename\> *のファイル id) に従う場合は、変更を減らす必要があります。

## <a name="to-create-a-registration-manifest"></a>登録マニフェストを作成するには

- **/Regfile**スイッチを使用して regpkg を実行します。 他のスイッチ、出力ファイルの名前、および VSPackage のパスを指定します。

     たとえば、コマンドプロンプトで、次のように入力します。

    ```
    <Visual Studio SDK installation path>\VisualStudioIntegration\Tools\Bin\RegPkg /regfile:MyRegFile.reg MyPackage.dll
    ```

## <a name="to-view-a-registration-manifest"></a>登録マニフェストを表示するには

- 任意のテキストエディターで登録マニフェストを開きます。

     次の例は、RegPkg が IronPython language サービス用に作成する登録マニフェストです。

    ```
    REGEDIT4

    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    "DisplayName"="131"
    "IndexPath"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\SnippetsIndex.xml"
    "LangStringId"="python"
    "Package"="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "ShowRoots"=dword:00000000
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\ForceCreateDirs]
    "Python"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\Paths]
    "Python"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}]
    @="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage, IronPython.LanguageService, Version=1.0.2373.36479, Culture=neutral, PublicKeyToken=null"
    "InprocServer32"="C:\\WINNT\\system32\\mscoree.dll"
    "Class"="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage"
    "Assembly"="IronPython.LanguageService, Version=1.0.2373.36479, Culture=neutral, PublicKeyToken=null"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\File Extensions]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\File Extensions\.py]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\Language Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\Language Services\Python]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    "Package"="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "LangResID"=dword:00000064
    "ShowMatchingBrace"=dword:00000001
    "CodeSense"=dword:00000001
    "MatchBraces"=dword:00000001
    "EnableCommenting"=dword:00000001
    "ShowCompletion"=dword:00000001
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}]
    "ID"=dword:00000001
    "MinEdition"="standard"
    "ProductVersion"="1.0"
    "ProductName"="Visual Studio Integration of IronPython Language Service"
    "CompanyName"="Microsoft Corporation"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services\{923b4811-26e4-4347-ac8a-244762798e1c}]
    @="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "Name"="IPythonLibraryManager"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services\{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}]
    @="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "Name"="Python"

    ```

## <a name="to-create-a-windows-installer-xml-toolset-include-file"></a>Windows インストーラー XML ツールセットインクルードファイルを作成するには

- **/Wixfile**スイッチを使用して regpkg を実行します。 他のスイッチ、出力ファイルの名前、および VSPackage のパスを指定します。

     たとえば、コマンドプロンプトで、次のように入力します。

    ```
    <Visual Studio SDK installation path>\VisualStudioIntegration\Tools\Bin\RegPkg /codebase /wixfile:IronPython.LanguageService.wxi ..\bin\Release\IronPython.LanguageService.dll
    ```

## <a name="to-view-a-windows-installer-xml-toolset-include-file"></a>Windows インストーラー XML ツールセットインクルードファイルを表示するには

- 任意のテキストエディターで Windows インストーラー XML ツールセットインクルードファイルを開きます。

     次の例は、RegPkg によって IronPython language サービス用に作成されるインクルードファイルです。

    ```xml
    <Include>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\IntellisenseProviders\IronPythonCodeProvider">
        <Registry Name="GUID" Value="{9c1807ea-d222-4775-afa8-c092c580e451}" Type="string" />
        <Registry Name="AddItemLanguageName" Value="Iron Python" Type="string" />
        <Registry Name="DefaultExtension" Value=".py" Type="string" />
        <Registry Name="ShortLanguageName" Value="IronPython;Python" Type="string" />
        <Registry Name="TemplateFolderName" Value="IronPython" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string">
        <Registry Name="DisplayName" Value="131" Type="string" />
        <Registry Name="IndexPath" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\SnippetsIndex.xml" Type="string" />
        <Registry Name="LangStringId" Value="python" Type="string" />
        <Registry Name="Package" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string" />
        <Registry Name="ShowRoots" Value="0" Type="integer" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\ForceCreateDirs">
        <Registry Name="Python" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\Paths">
        <Registry Name="Python" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\File Extensions\.py" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string" />

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\Language Services\Python" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string">
        <Registry Name="Package" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string" />
        <Registry Name="LangResID" Value="100" Type="integer" />
        <Registry Name="ShowCompletion" Value="1" Type="integer" />
        <Registry Name="ShowMatchingBrace" Value="1" Type="integer" />
        <Registry Name="CodeSense" Value="1" Type="integer" />
        <Registry Name="MatchBraces" Value="1" Type="integer" />
        <Registry Name="EnableCommenting" Value="1" Type="integer" />
        <Registry Name="DefaultToInsertSpaces" Value="1" Type="integer" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage, IronPython.LanguageService, Version=1.0.2394.27719, Culture=neutral, PublicKeyToken=null" Type="string">
        <Registry Name="InprocServer32" Value="[SystemFolder]mscoree.dll" Type="string" />
        <Registry Name="Class" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage" Type="string" />
        <Registry Name="CodeBase" Value="[#File_IronPython.LanguageService.dll]" Type="string" />
        <Registry Name="ID" Value="1" Type="integer" />
        <Registry Name="MinEdition" Value="standard" Type="string" />
        <Registry Name="ProductVersion" Value="1.0" Type="string" />
        <Registry Name="ProductName" Value="Visual Studio Integration of IronPython Language Service" Type="string" />
        <Registry Name="CompanyName" Value="Microsoft Corporation" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\CLSID\{9c1807ea-d222-4775-afa8-c092c580e451}" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonIntellisenseProvider" Type="string">
        <Registry Name="InprocServer32" Value="[SystemFolder]mscoree.dll" Type="string" />
        <Registry Name="Class" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonIntellisenseProvider" Type="string" />
        <Registry Name="CodeBase" Value="[#File_IronPython.LanguageService.dll]" Type="string" />
        <Registry Name="ThreadingModel" Value="Both" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Services\{923b4811-26e4-4347-ac8a-244762798e1c}" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string">
        <Registry Name="Name" Value="IPythonLibraryManager" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Services\{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string">
        <Registry Name="Name" Value="Python" Type="string" />
      </Registry>
    </Include>
    ```

## <a name="see-also"></a>こちらもご覧ください

- [Vspackage の登録](../../extensibility/registering-and-unregistering-vspackages.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
