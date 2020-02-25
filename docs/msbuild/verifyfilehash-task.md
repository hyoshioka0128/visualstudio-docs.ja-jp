---
title: VerifyFileHash タスク | Microsoft Docs
ms.date: 01/28/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- VerifyFileHash task [MSBuild]
- MSBuild, VerifyFileHash task
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9340657704900feb5ebdc188103109872ee39f5d
ms.sourcegitcommit: e3b9cbeea282f1b531c6a3f60515ebfe1688aa0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2020
ms.locfileid: "77439125"
---
# <a name="verifyfilehash-task"></a>VerifyFileHash タスク

ファイルが予想されるファイル ハッシュと一致することを確認します。 ハッシュが一致しない場合、タスクは失敗します。

このタスクは 15.8 で追加されましたが、16.0 より前の MSBuild バージョンで使用するには[回避策](https://github.com/Microsoft/msbuild/pull/3999#issuecomment-458193272)が必要です。

## <a name="task-parameters"></a>タスク パラメーター

 `VerifyFileHash` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`File`|必須の `String` 型のパラメーターです。<br /><br />ハッシュ値を計算し、検証するファイル。|
|`Hash`|必須の `String` 型のパラメーターです。<br /><br />予想されるファイル ハッシュ。|
|`Algorithm`|省略可能な `String` 型のパラメーターです。<br /><br />アルゴリズム。 許可値: `SHA256`、`SHA384`、`SHA512`。 既定値 = `SHA256`。|
|`HashEncoding`|省略可能な `String` 型のパラメーターです。<br /><br />生成されたハッシュに使用するエンコード。 既定値は `hex` です。 許可値 = `hex`、`base64`。|

## <a name="example"></a>例

次の例では、`VerifyFileHash` タスクを使用してそのチェックサムが検証されます。

```xml
<Project>
  <Target Name="VerifyHash">
    <GetFileHash Files="$(MSBuildProjectFullPath)">
      <Output
          TaskParameter="Items"
          ItemName="FilesWithHashes" />
    </GetFileHash>

    <Message Importance="High"
             Text="@(FilesWithHashes->'%(Identity): %(FileHash)')" />

    <VerifyFileHash File="$(MSBuildThisFileFullPath)"
                    Hash="$(ExpectedHash)" />
  </Target>
</Project>
```

MSBuild 16.5 以降では、ハッシュが一致しないときにビルドが失敗しないようにする場合 (たとえば、制御フローの条件としてハッシュ比較を使用している場合)、次のコードを使用して警告をメッセージにダウングレードできます。

```xml
  <PropertyGroup>
    <MSBuildWarningsAsMessages>$(MSBuildWarningsAsMessages);MSB3952</MSBuildWarningsAsMessages>
  </PropertyGroup>

  <Target Name="DemoVerifyCheck">
    <VerifyFileHash File="$(MSBuildThisFileFullPath)"
                    Hash="1"
                    ContinueOnError="WarnAndContinue" />

    <PropertyGroup>
      <HashMatched>$(MSBuildLastTaskResult)</HashMatched>
    </PropertyGroup>

    <Message Condition=" '$(HashMatched)' != 'true'"
             Text="The hash didn't match" />

    <Message Condition=" '$(HashMatched)' == 'true'"
             Text="The hash did match" />
  </Target>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
