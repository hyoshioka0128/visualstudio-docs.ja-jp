---
title: XslTransformation タスク | Microsoft Docs
description: MSBuild で、XslTransformation タスクを使用して、XSLT を使用した XML 入力の変換と出力デバイスまたはファイルへの出力を行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, XslTransformation task
- XslTransformation task [MSBuild]
ms.assetid: 6f3a7d81-3ae3-4703-9a06-870b32b69d80
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f779fc5d222fdd0985adef203f0bb20fc601a429
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847947"
---
# <a name="xsltransformation-task"></a>XslTransformation タスク

XSLT またはコンパイルされた XSLT を利用して XML 入力を変換し、出力デバイスまたはファイルに出力します。

## <a name="parameters"></a>パラメーター

 `XslTransformation` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`OutputPaths`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> XML 変換の出力ファイルを指定します。|
|`Parameters`|省略可能な `String` 型のパラメーターです。<br /><br /> XSLT 入力ドキュメントにパラメーターを指定します。  各パラメーターを `<Parameter Name="" Value="" Namespace="" />` として保持する未加工 XML が提供されます。|
|`XmlContent`|省略可能な `String` 型のパラメーターです。<br /><br /> XML 入力を文字列として指定します。|
|`XmlInputPaths`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> XML 入力ファイルを指定します。|
|`XslCompiledDllPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> コンパイルされた XSLT を指定します。|
|`XslContent`|省略可能な `String` 型のパラメーターです。<br /><br /> XSLT 入力を文字列として指定します。|
|`XslInputPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> XSLT 入力ファイルを指定します。|

## <a name="remarks"></a>解説

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

次の例では、xml ファイル `$(XmlInputFileName)` の変更に XSL 変換ファイル *transform.xslt* が使用されます。 変換された XML は `$(IntermediateOutputPath)output.xml` に書き込まれます。 XSL 変換では入力パラメーターとして `$(Parameter1)` が受け取られます。

```xml
    <XslTransformation XslInputPath="transform.xslt"
                       XmlInputPaths="$(XmlInputFileName)"
                       OutputPaths="$(IntermediateOutputPath)output.xml"
                       Parameters="&lt;Parameter Name='Parameter1' Value='$(Parameter1)'/&gt;"/>
```

## <a name="see-also"></a>関連項目

- [XSLT パラメーター](/dotnet/standard/data/xml/xslt-parameters)
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
