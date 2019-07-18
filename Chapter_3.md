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

There can be no real guarantees in procedural software. To name just one way of evading assertions, code could have additional side effects that were not specifically excluded. No matter how model-driven our design is, we still end up writing procedures to produce the effect of the conceptual interactions. And we spend much of our time writing boilerplate code that doesn’t really add any meaning or behavior. Intention-revealing interfaces and the other patterns in this chapter help, but they can never give conventional object-oriented programs formal rigor.

These are some of the motivations behind declarative design. This term means many things to many people, but usually it indicates a way to write a program, or some part of a program, as a kind of executable specification. A very precise description of properties actually controls the software. In its various forms, this could be done through a reflection mechanism or at compile time through code generation (producing conventional code automatically, based on the declaration). This approach allows another developer to take the declaration at face value. It is an absolute guarantee.

Many declarative approaches can be corrupted if the developers bypass them intentionally or unintentionally. This is likely when the system is difficult to use or overly restrictive. Everyone has to follow the rules of the framework in order to get the benefits of a declarative program.

#### A Declarative Style of Design

Once your design has intention-revealing interfaces, side-effect-free functions, and assertions, you are edging into declarative territory. Many of the benefits of declarative design are obtained once you have combinable elements that communicate their meaning, and have characterized or obvious effects, or no observable effects at all.

A supple design can make it possible for the client code to use a declarative style of design. To illustrate, the next section will bring together some of the patterns in this chapter to make the specification more supple and declarative.

### Drawing on Established Formalisms

Creating a tight conceptual framework from scratch is something you can’t do every day. Sometimes you discover and refine one of these over the course of the life of a project. But you can often use and adapt conceptual systems that are long established in your domain or others, some of which have been refined and distilled over centuries. Many business applications involve accounting, for example. Accounting defines a well-developed set of entities and rules that make for an easy adaptation to a deep model and a supple design.

There are many such formalized conceptual frameworks, but my personal favorite is math. It is surprising how useful it can be to pull out some twist on basic arithmetic. Many domains include math somewhere. Look for it. Dig it out. Specialized math is clean, combinable by clear rules, and people find it easy to understand.

A real-world example, “Shares Math,” was discussed in Chapter 8 of the book, Domain-Driven Design.

### Conceptual Contours

Sometimes people chop functionality fine to allow flexible combination. Sometimes they lump it large to encapsulate complexity. Sometimes they seek a consistent granularity, making all classes and operations to a similar scale. These are oversimplifications that don’t work well as general rules. But they are motivated by basic problems.

When elements of a model or design are embedded in a monolithic construct, their functionality gets duplicated. The external interface doesn’t say everything a client might care about. Their meaning is hard to understand, because different concepts are mixed together.

Conversely, breaking down classes and methods can pointlessly complicate the client, forcing client objects to understand how tiny pieces fit together. Worse, a concept can be lost completely. Half of a uranium atom is not uranium. And of course, it isn’t just grain size that counts, but just where the grain runs.

Therefore:

__Decompose design elements (operations, interfaces, classes, and aggregates) into cohesive units, taking into consideration your intuition of the important divisions in the domain. Observe the axes of change and stability through successive refactorings and look for the underlying conceptual contours that explain these shearing patterns. Align the model with the consistent aspects of the domain that make it a viable area of knowledge in the first place.__

A supple design based on a deep model yields a simple set of interfaces that combine logically to make sensible statements in the ubiquitous language, and without the distraction and maintenance burden of irrelevant options.
