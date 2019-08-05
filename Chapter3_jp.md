## III. Supple Design

開発が進行するにつれてプロジェクトを加速させるには、―独自の遺産に惑わされるのではなく、―変更を促しながら取り組むのが楽しいデザインが必要です。 しなやかなデザイン。

しなやかなデザインは深いモデリングを補完するものです。

開発者は2つの役割を果たしますが、それぞれを設計によって提供する必要があります。 同じ人が両方の役割を果たす可能性があります。数分で切り替えることもできますが、それでもコードとの関係は異なります。 1つの役割は、設計の機能を利用して、ドメインオブジェクトをアプリケーションコードまたは他のドメイン層のコードに織り込むクライアント開発者です。 しなやかなデザインは、その潜在力を明確にする深い基礎となるモデルを明らかにします。 クライアント開発者は、最小限の疎結合概念を柔軟に使用して、ドメイン内のさまざまなシナリオを表現できます。 構成要素は、予測可能で、明確に特徴付けられ、堅牢である結果を伴って、自然な方法で共々にフィットします。

同様に重要なことは、デザインはそれを変更するために働いている開発者に役立つべきです。 変更をオープンにするには、デザインは理解しやすいものでなければならず、クライアント開発者が描いているのと同じ基礎モデルを明らかにします。 それはドメインの深いモデルの輪郭に沿うものでなければならず、ほとんどの変更は設計の柔軟なポイントで行います。 そのコードの影響は透過的に明白でなければならないので、変更の結果は予想しやすいでしょう。

- 振る舞いを明確にする
- 変更のコストを下げる
- 共に開発できるソフトウェア開発者をつくる

### Intention-Revealing Interfaces

開発者がそれを使用するためにコンポーネントの実装を考慮しなければならない場合、カプセル化の価値は失われます。 元の開発者以外の誰かがその実装に基づいてオブジェクトまたは操作の目的を推測しなければならない場合、その新しい開発者はそのオペレーションやクラスが達成しようとする目的を全くの偶然でしか推測できません。 もしそれが意図された目的でないのであれば、コードは今のところ動作するかもしれませんが、設計の概念的な基礎は破壊され、2人の開発者は異なる方向性の中で作業することになるでしょう。

Therefore:

__期待動作と実装の意味を他に参照することなく、それらの効果と目的がわかるようにクラスとオペレーションに名前を付けます。 これにより、クライアント開発者は内部を理解する必要がなくなります。 チームメンバーがすぐにその意味を察知できるように、これらの名前はユビキタス言語に準拠している必要があります。 振る舞いを作成する前にテストを書いて、クライアント開発者モードに思考を強制します。__

### Side-Effect-Free Functions

Interactions of multiple rules or compositions of calculations become extremely difficult to predict. The developer calling an operation must understand its implementation and the implementation of all its delegations in order to anticipate the result. The usefulness of any abstraction of interfaces is limited if the developers are forced to pierce the veil. Without safely predictable abstractions, the developers must limit the combinatory explosion, placing a low ceiling on the richness of behavior that is feasible to build.

Therefore:

__Place as much of the logic of the program as possible into functions, operations that return results with no observable side effects. Strictly segregate commands (methods which result in modifications to observable state) into very simple operations that do not return domain information. Further control side effects by moving complex logic into value objects when a concept fitting the responsibility presents itself.__

__All operations of a value object should be side-effect-free functions.__

### Assertions

操作の副作用がそれらの実装によって暗黙のうちに定義されるだけであるとき、多くの委譲を持つデザインは原因と結果のもつれになります。 プログラムを理解する唯一の方法は、分岐パスを介して実行をトレースすることです。 カプセル化の価値は失われます。 具体的な実行をたどることの必要性は抽象化を無効にします。

Therefore:

__操作の事後条件とクラスおよび集合体の不変条件を記述します。 アサーションをプログラミング言語で直接コーディングできない場合は、それらに対して自動ユニットテストを記述してください。 プロジェクトの開発プロセスのスタイルに合うように、それらをドキュメントまたは図に書きます。__

開発者がアサーションの意図を察知し、学習曲線を加速し、矛盾するコードのリスクを減らすことができるようにするために、一貫した一連の概念を持つモデルを探します。

アサーションはサービスの契約とエンティティ修飾子を定義します。 アサーションは集約に対する不変条件を定義します。

### Standalone Classes

モジュール内であっても、依存関係が追加されるにつれて、デザインを解釈することの難しさは激しく増加します。 これは精神的な負荷を増し、開発者の扱う設計の複雑性の許容範囲を弱めます。 暗黙の概念は明示的な参照よりも、この負荷を増加します。

__低結合は、オブジェクト設計の基本です。 可能であれば、ずっと行ってください。 クラスの設計書から他のすべての概念を取り除きます。 その後、クラスは完全に自己完結型になり、一人で学習し理解することができます。 そのような自己完結型のクラスはすべて、モジュール理解の負担を大幅に軽減します。__

### Closure of Operations

興味深いことに、オブジェクトは、プリミティブだけでは特徴づけられないことをすることができるようになります。

Therefore:

__Where it fits, define an operation whose return type is the same as the type of its argument(s). If the implementer has state that is used in the computation, then the implementer is effectively an argument of the operation, so the argument(s) and return value should be of the same type as the implementer. Such an operation is closed under the set of instances of that type. A closed operation provides a high-level interface without introducing any dependency on other concepts.__

This pattern is most often applied to the operations of a value object. Because the life cycle of an entity has significance in the domain, you can’t just conjure up a new one to answer a question. There are operations that are closed under an entity type. You could ask an Employee object for its supervisor and get back another Employee. But in general, entities are not the sort of concepts that are likely to be the result of a computation. So, for the most part, this is an opportunity to look for in the value objects.

You sometimes get halfway to this pattern. The argument matches the implementer, but the return type is different, or the return type matches the receiver and the argument is different. These operations are not closed, but they do give some of the advantage of closure, in freeing the mind.

### Declarative Design

手続き型ソフトウェアには本当の保証はありません。 アサーションを回避するための1つの方法だけを挙げると、コードには特に除外されていない追加の副作用があります。 モデル駆動型の設計がどのようなものであっても、概念上の相互作用の効果を生み出すための手順を書くことになります。 そして、私たちは時間をかけて、意味や動作を追加することのない定型コードを書いています。 この章の意図を明らかにするインターフェースやその他のパターンは役に立ちますが、従来のオブジェクト指向プログラムを形式的に厳密にすることはありません。

これらは宣言的デザインの背後にある動機のいくつかです。 この用語は多くの人にとって多くのことを意味しますが、通常はプログラム、またはプログラムの一部を一種の実行可能仕様として書く方法を示します。 プロパティの非常に正確な説明が実際にソフトウェアを制御します。 さまざまな形式で、これはリフレクションメカニズムを通じて、またはコード生成を通じてコンパイル時に（宣言に基づいて従来のコードを自動的に生成することによって）行うことができます。 このアプローチにより、他の開発者は宣言を書いてあるとおりに受け取ります。 絶対的な保証です。

開発者が意図的・意図しないにかかわらず、それらを回避すると、多くの宣言型アプローチが破損する可能性があります。 これは、システムの使用が難しい、または過度に制限が厳しい場合に発生する可能性があります。 宣言型プログラムの恩恵を受けるためには、誰もがフレームワークの規則に従わなければなりません。

#### A Declarative Style of Design

あなたのデザインが意図を明らかにするインターフェース、副作用のない関数、そしてアサーションを持っていると、あなたは宣言的領域に近づいています。 宣言的デザインの利点の多くは、それらの意味を伝える組み合わせ可能な要素があり、特徴的または明白な効果がある、またはまったく観察可能な効果がない場合に得られます。

柔軟な設計では、クライアントコードで宣言型の設計を使用できます。 説明のために、次のセクションでは、この章のいくつかのパターンをまとめて、仕様をより柔軟で宣言的なものにします。

### Drawing on Established Formalisms

厳密な概念的フレームワークをゼロから作成することは、毎日できないことです。 時にはあなたはプロジェクトの人生の過程でこれらの一つを発見しそして改良する。 しかし、あなたは自分の分野や他の分野で長い間確立されてきた概念的システムをしばしば使用し適応させることができます。そのいくつかは何世紀にもわたって洗練され蒸留されてきました。 たとえば、多くのビジネスアプリケーションには会計が含まれます。 会計は、深いモデルと柔軟な設計への容易な適応を可能にする、よく開発されたエンティティと規則のセットを定義します。

そのような形式化された概念的フレームワークはたくさんありますが、私の個人的なお気に入りは数学です。 基本的な算術を少し工夫することがいかに役に立つかは驚くべきことです。 多くのドメインはどこかに数学を含んでいます。 それを探す。 それを掘り出しなさい。 専門の数学はきれいで、明確な規則と組み合わせることができ、人々はそれを理解するのが簡単だと感じます。

実例「Shares Math」は、本の第8章「Domain-Driven Design」で説明されています。

### Conceptual Contours

時々人々は柔軟な組み合わせを可能にするために機能性を細かく刻みます。 時には彼らは複雑さをカプセル化するためにそれを大きくまとめます。 時には彼らは一貫した粒度を求め、すべてのクラスとオペレーションを同じ規模にします。 これらは一般的なルールとしてはうまく機能しない単純化しすぎです。 しかし、それらは基本的な問題によって動機付けられています。

モデルやデザインの要素がモノリシック構造に埋め込まれていると、それらの機能は重複します。 外部インターフェースは、クライアントが気にするかもしれないことすべてを言うわけではありません。 異なる概念が混在しているので、それらの意味は理解するのが難しいです。

逆に、クラスやメソッドを細かく分割するとクライアントが無意味に複雑になる可能性があり、クライアントオブジェクトに小さな部分がどのように適合するかを理解させることになります。 さらに悪いことに、概念は完全に失われる可能性があります。 ウラン原子の半分はウランではありません。 もちろん、重要なのはグレインサイズだけではなく、グレインが流れる場所だけです。

Therefore:

__ドメイン内の重要な部門に関する直感を考慮しながら、設計要素（オペレーション、インターフェース、クラス、および集合体）をまとまりのある単位に分解します。 連続的なリファクタリングを通じて変化の軸と安定性を観察し、これらのせん断パターンを説明する根本的な概念的な輪郭を探します。 そもそもそれを実行可能な知識の領域にするドメインの一貫した側面にモデルを合わせます。__

深いモデルに基づくしなやかな設計は、ユビキタスな言語で理にかなったステートメントを作るために論理的に結合して、無関係なオプションの気を散らすこととメンテナンスの負担なしで、単純なインタフェースのセットを生み出します。