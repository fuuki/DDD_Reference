## V. Distillation for Strategic Design

中心的な問題に焦点を当て、副次的な問題の海に溺れないようにするにはどうすればよいでしょうか？

蒸留は、混合物となったコンポーネントを分離して、それをより価値があり有用になる形でエッセンスを抽出するプロセスです。 モデルは知識の蒸留です。 より深い洞察へのリファクタリングのたびに、ドメイン知識と優先順位のいくつかの重要な側面を抽象化します。 さて、戦略的な見方に戻って、この章ではモデルの広い範囲を区別してドメインモデル全体を蒸留する方法を見てみましょう。

### Core Domain

大規模システムではたくさんのコントリビュートされたコンポーネントがあり、それらは複雑で、成功させるために絶対に不可欠です。そのため、ドメインモデルのエッセンス、つまり実際のビジネス資産の本質は不明瞭になり無視される可能性があります。

デザインのすべての部分が同じように洗練されているわけではないというのは厳しい現実です。 優先順位を設定する必要があります。 ドメインモデルをアセットにするには、そのモデルの重要なコアを洗練され、十分に活用してアプリケーション機能を作成する必要があります。 しかし、高度なスキルを持つ一部の開発者は、専門的なドメイン知識を必要としないような技術的インフラストラクチャ、もしくは正確に定義可能なドメインの問題にだけ惹きつけられる傾向があります。

Therefore:

__モデルを煮詰めましょう。 コアドメインを定義し、それをサポートモデルやコードの大部分と容易に区別できるようにしましょう。 最も価値のある特化した概念をシャープな拠り所にしてください。 コアを小さくします。__

__最高の叡智をコアドメインに集め、そのために人を集めましょう。 システムのビジョンを満たすのに十分な、深いモデルを見つけ、しなやかな設計を開発するために、コアに努力を注いでください。__

コア以外の部分への評価は、それが蒸留されたコアをどのようにサポートするのかで決まります。

### Generic Subdomains

専門知識を捉えたり伝えたりすることがないモデルの一部分が、複雑さを増しているように見えることがあるでしょう。 無関係なものがあると、コアドメインを見て取ることや理解が困難になります。 誰もが知っている一般原則、または主な焦点ではないが補助的な役割を果たす専門分野に属する詳細は読み手を悩ませてくるでしょう。 それでも、一般的ではありますが、これらの他の要素は、システムの機能とモデルの完全な表現に不可欠です。

Therefore:

__プロジェクトのモチベーションではないまとまりのあるサブドメインを特定しましょう。 これらのサブドメインの一般的なモデルを取り除き、それらを別々のモジュールに配置します。 それらにあなたの専門の痕跡を残さないでください。__

__分離したら、継続的な開発をコアドメインよりも優先度を低くし、コア開発者をタスクに割り当てないようにします（ドメインの知識がほとんど得られないため）。 これらの一般的なサブドメイン用の既製のソリューションや公開モデルも検討してください。__

### Domain Vision Statement

プロジェクトの開始時には、通常、モデルは存在していませんが、その開発に集中する必要性はすでにあります。 開発の後半の段階では、モデルの詳細な調査を必要としないシステムの価値の説明が必要です。 また、ドメインモデルの重要な側面は、境界のある複数のコンテキストにまたがる可能性がありますが、定義上、これらの異なるモデルは共通のフォーカスを持つように構成してはいけません。

Therefore:

__コアドメインとそれがもたらす価値、つまり「価値命題」の簡単な説明（約1ページ）を書きます。このとき、ドメインモデルとその他を区別しない側面は無視してください。 ドメインモデルが多様な利益をどのように提供しバランスをとるかを示します。 狭くしてください。 この文を早い段階で書き、新しい洞察を得たら修正してください。__

### Highlighted Core

ドメインビジョンステートメントは、コアドメインを広い意味で識別しますが、コアモデル要素の詳しい識別は個々の解釈により食い違いが生じます。 チームに非常にレベルの高いコミュニケーションがない限り、ビジョンステートメントだけではほとんど影響がありません。

チームメンバーがコアドメインを構成する要素を広く知っている場合でも、さまざまな人がまったく同じ要素を選び取ることはないでしょうし、同じ人であっても一貫していないことがあります。 重要な部分を識別するためにモデルを絶えずフィルタリングするという精神的な労力は、集中力が必要な設計思想と、モデルに関する包括的な知識が必要です。 コアドメインは見やすくする必要があります。

コードに対する大幅な構造上の変更は、コアドメインを識別するための理想的な方法ですが、短期的には必ずしも実用的ではありません。 実際、このような大きなコード変更は、チームが未熟だという酷な見方なしには実行するのが困難です。

Therefore (as one form of highlighted core):

__コアドメインとコア要素間の主要な相互作用について説明した非常に短い文書（3〜7つの疎なページ）を書いてください。__

and/or (as another form of highlighted core):

__特にその役割を解明しようとすることなく、モデルのプライマリリポジトリ内のコアドメインの要素にフラグを付けます。 開発者がコアの内外に何があるのか簡単に知ることができるようにします。__

If the distillation document outlines the essentials of the core domain, then it serves as a practical indicator of the significance of a model change. When a model or code change affects the distillation document, it requires consultation with other team members. When the change is made, it requires immediate notification of all team members, and the dissemination of a new version of the document. Changes outside the core or to details not included in the distillation document can be integrated without consultation or notification and will be encountered by other members in the course of their work. Then the developers have the full autonomy that most Agile processes suggest.

_Although the vision statement and highlighted core inform and guide, they do not actually modify the model or the code itself. Partitioning generic subdomains physically removes some distracting elements. Next we’ll look at other ways to structurally change the model and the design itself to make the core domain more visible and manageable...._

### Cohesive Mechanisms

計算の複雑さのレベルは、設計の肥大化を招くほどになる場合があります。 概念的な「何を (what)」は、機構的な「どうやって (how)」によって埋没させられます。問題を解決するためのアルゴリズムを提供する多数の方法は、問題を表現する方法を不明瞭にします。

Therefore:

__概念的にまとまりのあるメカニズムを別の軽量フレームワークに分割します。 特に形式化や文書化されたアルゴリズムのカテゴリに注目してください。 意図を明らかにするインターフェースでフレームワークによって可能となることを明示します。 このドメインの他の要素は、問題の表現（ "what"）に焦点を当て、ソリューションの複雑さ（ "how"）をフレームワークに任せることができます。__

__Factoring out generic subdomains reduces clutter, and cohesive mechanisms serve to encapsulate complex operations. This leaves behind a more focused model, with fewer distractions that add no particular value to the way users conduct their activities. But you are unlikely ever to find good homes for everything in the domain model that is not core. The segregated core takes a direct approach to structurally marking off the core domain...__

### Segregated Core

モデル内の要素は、コアドメインを部分的に提供し、部分的に補助的な役割を果たします。 コア要素は、一般的な要素と密接に関連している可能性があります。 コアの概念的なまとまりははっきりとせず、見えづらいかもしれません。 この雑然とした絡み合いのすべてがコアを覆い隠します。 設計者は最も重要な関係を明確に理解できず、弱いデザインにつながります。

Therefore:

__モデルをリファクタリングして、中核となる概念と他のコードとの結び付きを減らしながら、サポートしているプレイヤー（明確でないものも含む）から分離し、コアの凝縮度を強化します。 たとえこれが、高度に結合された要素の分離することでしか実現できないモデルのリファクタリングだとしても、すべての一般的な要素・サポートする要素を他のオブジェクトに分解して他のパッケージに配置します。__

### Abstract Core

コアドメインモデルでさえ、多くの場合は詳細が非常に多いため、全体像を伝えることは困難です。

別々のモジュール内のサブドメイン間で多くの相互作用がある場合は、モジュール間で多数の参照を作成しなければならない（パーティショニングの価値の大部分を失う）、または相互作用を間接的にしなければならないため、モデルが不明瞭になります。

Therefore:

__モデル内で最も基本的な差別化概念を識別し、それらを別々のクラス、抽象クラス、またはインターフェースに分解します。 重要なコンポーネント間の相互作用のほとんどを表すように、この抽象モデルを設計してください。 この抽象的な全体モデルを独自のモジュールに配置します。一方、特殊で詳細な実装クラスは、サブドメインによって定義された独自のモジュールに残ります。__
