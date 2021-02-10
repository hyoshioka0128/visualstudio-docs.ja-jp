---
title: GetFileHash タスク | Microsoft Docs
description: MSBuild GetFileHash タスクを使用して、ファイルまたは一連のファイルの内容のチェックサムを計算する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/28/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFileHash task [MSBuild]
- MSBuild, GetFileHash task
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 163fbfd9c2bf0ca56b5b9b6bc11dc48420cfc270
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914698"
---
# <a name="getfilehash-task"></a>GetFileHash タスク

1 つのファイルまたはファイルのセットの内容のチェックサムを計算します。

このタスクは 15.8 で追加されましたが、16.0 より前の MSBuild バージョンで使用するには[回避策](https://github.com/Microsoft/msbuild/pull/3999#issuecomment-458193272)が必要です。

## <a name="task-parameters"></a>タスク パラメーター

 `GetFileHash` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`Files`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br />ハッシュするファイル。|
|`Items`|<xref:Microsoft.Build.Framework.ITaskItem>`[]` 出力パラメーターです。<br /><br />`Files` 入力と、ファイル ハッシュに設定された追加メタデータ。|
|`Hash`|`String` 出力パラメーターです。<br /><br />ファイルのハッシュ。 この出力は、項目が厳密に 1 個渡された場合にのみ設定されます。|
|`Algorithm`|省略可能な `String` 型のパラメーターです。<br /><br />アルゴリズム。 許可値: `SHA256`、`SHA384`、`SHA512`。 既定値 = `SHA256`。|
|`MetadataName`|省略可能な `String` 型のパラメーターです。<br /><br />メタデータ名。この場所で、各項目にハッシュが保管されます。 既定値は `FileHash` です。|
|`HashEncoding`|省略可能な `String` 型のパラメーターです。<br /><br />生成されたハッシュに使用するエンコード。 既定値は `hex` です。 許可値 = `hex`、`base64`。|

## <a name="example"></a>例

次の例では、`GetFileHash` タスクを使用して `FilesToHash` 項目のチェックサムが決定され、出力されます。

```xml
<Project>
  <ItemGroup>
    <FilesToHash Include="$(MSBuildThisFileDirectory)\*" />
  </ItemGroup>
  <Target Name="GetHash">
    <GetFileHash Files="@(FilesToHash)">
      <Output
          TaskParameter="Items"
          ItemName="FilesWithHashes" />
    </GetFileHash>

    <Message Importance="High"
             Text="@(FilesWithHashes->'%(Identity): %(FileHash)')" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)