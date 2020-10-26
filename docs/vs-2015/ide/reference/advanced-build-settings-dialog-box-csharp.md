---
title: '[ビルドの詳細設定] ダイアログ ボックス (C#) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 38f4d233c8804bec91d2f7dfd2dc34c6879e8be9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651732"
---
# <a name="advanced-build-settings-dialog-box-c"></a>[ビルドの詳細設定] ダイアログ ボックス (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー**の **[ビルドの詳細設定]** ダイアログ ボックスを使用して、プロジェクトの詳細なビルド構成プロパティを指定します。 このダイアログ ボックスは、[!INCLUDE[csprcs](../../includes/csprcs-md.md)] プロジェクトにのみ適用されます。

## <a name="general"></a>全般
 次のオプションを使用すると、全般的な詳細設定を有効にできます。

 **言語バージョン** 使用する言語のバージョンを指定します。 機能セットはバージョンによって異なるので、このオプションを使用して、コンパイラが特定の実装機能のみを許可するように強制したり、既存の標準と互換性のある機能のみを有効にしたりすることができます。 この設定には、次のオプションがあります。

- **ISO-1**

   ISO-1 の標準機能をターゲットにします。

- **default**

   現在のバージョンをターゲットにします。

  詳細については、「 [/langversion (C# コンパイラオプション)](https://msdn.microsoft.com/library/3fb00b05-a0ff-4782-b313-13a4c0f62d94)」を参照してください。

  **内部コンパイル エラー報告** コンパイラ エラーを Microsoft に報告するかどうかを指定します。 **prompt** (既定) に設定すると、内部コンパイラ エラーが発生した場合にプロンプトが表示され、エラー報告を電子的に Microsoft に送信するオプションが示されます。 **send** に設定すると、エラー報告は自動的に送信されます。 **queue** に設定すると、報告はキューに追加されます。 **none** に設定すると、エラーはコンパイラのテキスト出力にのみ報告されます。 詳細については、「 [/errorreport (C# コンパイラオプション)](https://msdn.microsoft.com/library/bd0e7493-b79d-4369-9c3f-ba26ebdfbedf)」を参照してください。

  **算術オーバーフローまたはアンダーフローのチェック**[Checked](https://msdn.microsoft.com/library/718a1194-988d-48a3-b089-d6ee8bd1608d)または[unchecked](https://msdn.microsoft.com/library/0c021f7c-923f-4b3d-a58f-55336f5ac27e)キーワードのスコープ内に含まれない整数の算術ステートメントで、データ型の範囲外の値になる場合に、実行時の例外を発生させるかどうかを指定します。詳細については、「 [/checked (C# コンパイラオプション)](https://msdn.microsoft.com/library/fb7475d3-e6a6-4e6d-b86c-69e7a74c854b)」を参照してください。

  **mscorlib.dll を参照しない**<xref:System> 名前空間全体を定義して、mscorlib.dll をプログラムにインポートするかどうかを指定します。 独自の <xref:System> 名前空間およびオブジェクトを定義または作成する場合は、このチェック ボックスをオンにします。 詳細については、「 [/nostdlib (C# コンパイラオプション)](https://msdn.microsoft.com/library/ec197989-fa49-4725-a455-e06b551eb65f)」を参照してください。

## <a name="output"></a>出力
 次のオプションを使用すると、詳細な出力オプションを指定できます。

 **デバッグ情報** コンパイラによって生成されるデバッグ情報の種類を指定します。 アプリケーションのデバッグ パフォーマンスを構成する方法については、「[イメージのデバッグの簡略化](https://msdn.microsoft.com/library/7d90ea7a-150f-4f97-98a7-f9c26541b9a3)」を参照してください。 この設定には、次のオプションがあります。

- "**なし**"

   デバッグ情報を生成しないことを指定します。

- **full**

   実行中のプログラムにデバッガーをアタッチできるようにします。

- **pdbonly**

   プログラムがデバッガーで開始されたとき、ソース コードのデバッグが有効になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブラーが表示されます。

  詳細については、「 [/debug (C# コンパイラオプション)](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)」を参照してください。

  **ファイルの配置** 出力ファイル内のセクションのサイズを指定します。 有効な値は、 **512**、 **1024**、 **2048**、 **4096**、および **8192**です。 これらの値の単位はバイトです。 各セクションは、この値の倍数である境界内にアラインされるので、出力ファイルのサイズに影響があります。 詳細については、「 [/filealign (C# コンパイラオプション)](https://msdn.microsoft.com/library/15cf1c98-3798-4ced-9f08-60619308a073)」を参照してください。

  **DLL のベースアドレス** DLL を読み込む位置に推奨されるベースアドレスを指定します。 DLL の既定のベース アドレスは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイムにより設定されます。 詳細については、「 [/baseaddress (C# コンパイラオプション)](https://msdn.microsoft.com/library/ce13c965-dfe4-4433-94f5-63b476e3a608)」を参照してください。

## <a name="see-also"></a>参照
 [C# コンパイラ オプション](https://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44) [[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)
