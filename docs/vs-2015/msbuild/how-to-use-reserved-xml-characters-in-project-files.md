---
title: '方法: 予約済みの XML 文字をプロジェクト ファイルで使用する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, using reserved XML characters
- MSBuild, reserved XML characters
ms.assetid: 1ae37275-96bf-4e6e-897b-6b048e5bbe93
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aba17e94486ca04e12055c7bf9959f927440c53d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178315"
---
# <a name="how-to-use-reserved-xml-characters-in-project-files"></a>方法 : 予約済みの XML 文字をプロジェクト ファイルで使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクト ファイルを作成するときに、たとえばプロパティ値やタスク パラメーター値の中で、予約済み XML 文字を使用する必要が生じることがあります。 しかし、いくつかの予約文字は、プロジェクト ファイルを解析できるようにするために、名前付きエンティティに置き換える必要があります。  
  
## <a name="using-reserved-characters"></a>予約文字の使用  
 次の表は、プロジェクト ファイルを解析できるようにするために、対応する名前付きエンティティに置き換える必要がある予約済み XML 文字を示しています。  
  
|予約文字|名前付きエンティティ|  
|------------------------|------------------|  
|\<|&lt;|  
|>|&gt;|  
|&|&amp;|  
|"|&quot;|  
|'|&apos;|  
  
#### <a name="to-use-double-quotes-in-a-project-file"></a>プロジェクト ファイルで二重引用符を使用するには  
  
- 二重引用符を対応する名前付きエンティティ &quot; に置き換えます。 たとえば、`EXEFile` 項目リストを二重引用符で囲むには、次のように入力します。  
  
    ```  
    <Message Text="The output file is "@(EXEFile)"."/>  
    ```  
  
## <a name="example"></a>例  
 次のコード例では、プロジェクト ファイルによって出力されるメッセージの中でファイル名を強調するために二重引用符が使用されています。  
  
```  
<Project DefaultTargets="Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>"HelloWorldCS"</appname>  
    </PropertyGroup>  
    <!-- Specify the inputs -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs" />  
    </ItemGroup>  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input  
        files of type CSFile -->  
        <Csc Sources = "@(CSFile)">  
            <!-- Set the OutputAssembly attribute of the CSC task  
            to the name of the executable file that is created -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile"/>  
        </Csc>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is "@(EXEFile)"."/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md) [MSBuild](msbuild.md)
