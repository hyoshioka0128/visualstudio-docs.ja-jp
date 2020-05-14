---
title: レガシ言語サービスでのコードのコメント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5450199fde29f581dafdf9b2884c88ef26ea4ce7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709436"
---
# <a name="comment-code-in-a-legacy-language-service"></a>レガシ言語サービスのコメント コード
プログラミング言語は、通常、コードに注釈を付けたりコメントしたりするための手段を提供します。 コメントは、コードに関する追加情報を提供するテキストのセクションですが、コンパイルまたは解釈中に無視されます。

 管理パッケージ フレームワーク (MPF) クラスは、選択したテキストのコメントとコメント解除をサポートします。

## <a name="comment-styles"></a>コメントスタイル
コメントには、一般的なスタイルが 2 つあります。

1. コメントが 1 行に含まれます。

2. コメントをブロックします(コメントには複数行が含まれる場合があります)。

通常、行のコメントには開始文字 (または文字) が含まれ、ブロック コメントには開始文字と終了文字の両方が含まれます。 たとえば、C# では、行コメントが`//`で始まり、ブロック コメントが`/*`で始`*/`まり、ブロック コメントが で終わります。

ユーザーが **[詳細**編集 **]** > メニューから[**コメント選択**]コマンドを選択すると、そのコマンドは<xref:Microsoft.VisualStudio.Package.Source>クラス<xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A>のメソッドにルーティングされます。 ユーザーが [Select の**コメントを解除]** コマンドを選択すると、<xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A>コマンドはメソッドにルーティングされます。

## <a name="support-code-comments"></a>サポート コード コメント
 言語サービス サポート コードコメントは、 の名前付`EnableCommenting`きパラメーターを使用<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>して行うことができます。 クラスのプロパティ<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A>を<xref:Microsoft.VisualStudio.Package.LanguagePreferences>設定します。 言語サービス機能の設定の詳細については、「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください。

 また、このメソッドを<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>オーバーライドして、使用<xref:Microsoft.VisualStudio.Package.CommentInfo>している言語のコメント文字を含む構造体を返す必要があります。 C# スタイルの行コメント文字が既定です。

### <a name="example"></a>例
 メソッドの実装例を次に<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>示します。

```csharp
using Microsoft.VisualStudio.Package;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override CommentInfo GetCommentFormat() {
            CommentInfo info = new CommentInfo();
            info.LineStart       = "//";
            info.BlockStart      = "/*";
            info.BlockEnd        = "*/";
            info.UseLineComments = true;
            return info;
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービス機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service1.md)
