---
title: FXC タスク | Microsoft Docs
description: MSBuild FXC タスクがビルド プロセスで HLSL シェーダー コンパイラ用に使用するパラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.fxc
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), FXC task
- FXC task (MSBuild (C++))
author: corob-msft
ms.author: corob
ms.workload:
- multiple
ms.openlocfilehash: b200fde9e5bc07f654ae2bf11cd8a752efbfe123
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436691"
---
# <a name="fxc-task"></a>FXC タスク

ビルド プロセスで HLSL シェーダー コンパイラを使用します。

## <a name="parameters"></a>パラメーター

以下の表で、 **FXC** タスクのパラメーターについて説明します。

|パラメーター|[説明]|
|---------------|-----------------|
|**AdditionalIncludeDirectories**|省略可能な **string[]** 型のパラメーターです。<br/><br/>インクルード パスに追加するディレクトリを 1 つ以上指定します。複数指定する場合には、セミコロンで区切ってください。<br/><br/>`/I[path]` を使用してください。|
|**AdditionalOptions**|省略可能な **string** 型のパラメーターです。|
|**AllResourcesBound**|省略可能な **bool** 型のパラメーターです。<br/><br/>コンパイラでは、シェーダーの実行中、シェーダーが参照する可能性のあるすべてのリソースがバインドされ、良好な状態にあると仮定されます。 シェーダー モデル 5.1 以降で利用できます。<br/><br/>`/all_resources_bound` を使用してください。|
|**AssemblerOutput**|省略可能な **string** 型のパラメーターです。<br/><br/>アセンブリ言語の出力ファイルの内容を指定します。<br/><br/>`/Fc, /Fx` を使用してください。<br/><br/>**NoListing** <br/>**AssemblyCode** : `Fc` を使います。<br/>**AssemblyCodeAndHex** : `Fx` を使います。|
|**AssemblerOutputFile**|省略可能な **string** 型のパラメーターです。<br/><br/>アセンブリ コード リスティング ファイルの名前を指定します。|
|**CompileD2DCustomEffect**|省略可能な **bool** 型のパラメーターです。<br/><br/>ピクセル シェーダーを含む Direct2D カスタム効果をコンパイルします。 頂点に対して使ったり、カスタム効果を計算したりしないでください。|
|**ConsumeExportFile**|省略可能な **string** 型のパラメーターです。|
|**DisableOptimizations**|省略可能な **bool** 型のパラメーターです。<br/><br/>最適化を無効にします。<br/><br/>`/Od` は `/Gfp` を暗黙的に示しますが、出力は `/Od /Gfp` と同じにならない場合があります。|
|**EnableDebuggingInformation**|省略可能な **bool** 型のパラメーターです。<br/><br/>デバッグ情報を有効にします。|
|**EnableUnboundedDescriptorTables**|省略可能な **bool** 型のパラメーターです。<br/><br/>シェーダーにバインド解除済みの範囲のあるリソース配列の宣言が含まれている可能性があることをコンパイラに通知します。 シェーダー モデル 5.1 以降で利用できます。<br/><br/>`/enable_unbounded_descriptor_tables` を使用してください。|
|**EntryPointName**|省略可能な **string** 型のパラメーターです。<br/><br/>シェーダーのエントリ ポイント名を指定します。<br/><br/>`/E[name]` を使用してください。|
|**GenerateExportFile**|省略可能な **string** 型のパラメーターです。|
|**GenerateExportShaderProfile**|省略可能な **string** 型のパラメーターです。|
|**HeaderFileOutput**|省略可能な **string** 型のパラメーターです。<br/><br/>オブジェクト コードを含むヘッダー ファイル名を指定します。<br/><br/>`/Fh [name]` を使用してください。|
|**ObjectFileOutput**|省略可能な **string** 型のパラメーターです。<br/><br/>オブジェクト ファイル名を指定します。<br/><br/>`/Fo [name]` を使用してください。|
|**PreprocessorDefinitions**|省略可能な **string[]** 型のパラメーターです。<br/><br/>ソース ファイルの前処理シンボルを定義します。|
|**SetRootSignature**|省略可能な **string** 型のパラメーターです。<br/><br/>ルート署名をシェーダーのバイトコードに添付します。 Shader Model 5.0 以上で使用できます。<br/><br/>`/setrootsignature` を使用してください。|
|**ShaderModel**|省略可能な **string** 型のパラメーターです。<br/><br/>シェーダー モデルを指定します。 いくつかのシェーダーの種類は最新のシェーダー モデルでしか使用できません。<br/><br/>`/T [type]_[model]` を使用してください。|
|**ShaderType**|省略可能な **string** 型のパラメーターです。<br/><br/>シェーダーの種類を指定します。<br/><br/>`/T [type]_[model]` を使用してください。<br/><br/>**Effect** : `fx` を使います。<br/>**Vertex** : `vs` を使います。<br/>**Pixel** : `ps` を使います。<br/>**Geometry** : `gs` を使います。<br/>**Hull** : `hs` を使います。<br/>**Domain** : `ds` を使います。<br/>**Compute** : `cs` を使います。<br/>**Library** : `lib` を使います。<br/>**RootSignature** : ルート署名オブジェクトを生成します。|
|**ソース**|必須の **ITaskItem** 型のパラメーターです。|
|**SuppressStartupBanner**|省略可能な **bool** 型のパラメーターです。<br/><br/>著作権情報と情報メッセージを表示しません。<br/><br/>`/nologo` を使用してください。|
|**TrackerLogDirectory**|省略可能な **string** 型のパラメーターです。|
|**TreatWarningAsError**|省略可能な **bool** 型のパラメーターです。<br/><br/>コンパイラ警告をすべてエラーとして扱います。<br/><br/>新しいプロジェクトの場合、すべてのコンパイルで `/WX` を使用することをお勧めします。すべての警告を解決することで、見つけにくいコードの欠陥を最少に抑えられます。|
|**VariableName**|省略可能な **string** 型のパラメーターです。<br/><br/>ヘッダー ファイル内の変数名に対する名前を指定します。<br/><br/>`/Vn [name]` を使用してください。|

## <a name="see-also"></a>関連項目

[タスク リファレンス](../msbuild/msbuild-task-reference.md)