## IV.Context Mapping for Strategic Design

#### bounded context

特定のモデルが定義され適用可能な境界の説明（通常はサブシステム、または特定のチームの作業）。

#### upstream-downstream

「上流」グループの行動が「下流」グループのプロジェクトの成功に影響を与えるが、下流の行動が上流のプロジェクトに大きな影響を与えない2つのグループ間の関係。 （たとえば、2つの都市が同じ川沿いにある場合、上流の都市の汚染は主に下流の都市に影響を与えます。）

上流のチームは下流のチームの運命とは無関係に成功するかもしれない。

#### mutually dependent

2つの別々のコンテキストのソフトウェア開発プロジェクトが成功と見なされるためには、両方が提供される必要があるという状況。（2つのシステムがお互いの情報や機能に依存している場合 - 私たちが一般的に避けようとしていること - 自然にそれらを相互依存として構築するプロジェクトを見ます。しかしシステム依存が一方向のみを走る相互依存プロジェクトもあります。 依存型システムとそのシステムとの統合がなければ、依存型システムにはほとんど価値がありません - おそらくこれが唯一の使用場所であるため、依存型システムの提供に失敗すると、両方のプロジェクトが失敗することになります。)

#### free

A software development context in which the direction, success or failure of development work in other contexts has little effect on delivery.

### Context Map

戦略を描くためには、私たちのプロジェクトと私たちが統合している他の人とにまたがる現実的で大規模なモデル開発の見方が必要です。

グローバルな見解がない場合、個々の境界のある文脈はいくつかの問題を残します。 他のモデルのコンテキストはまだ曖昧で流動的かもしれません。

他のチームの人々はコンテキストの境界をあまり意識しておらず、知らないうちに境界をぼかしたり相互接続を複雑にしたりするような変更を加えるでしょう。 異なるコンテキスト間で接続を確立する必要がある場合、それらは互いを傷つけ合う傾向があります。

境界線がはっきりしていても、他の文脈との関係は、実現可能なモデルの性質または変化のペースに制約を課します。 これらの制約は、主に非技術的なチャネルを通じて明らかになり、それらが影響を及ぼしている設計の判断に関連させるのが難しいことがあるでしょう。

Therefore:

__プロジェクトで機能している各モデルを識別し、その境界のあるコンテキストを定義します。 これには、非オブジェクト指向サブシステムの暗黙のモデルも含まれます。 それぞれの境界のある文脈に名前を付け、その名前をユビキタス言語の一部にします。__

__モデル間の接点を説明し、コミュニケーションのための明示的な翻訳を概説し、共有、孤立メカニズム、影響力のレベルを強調する。__

__既存の地形をマッピングします。 後に変容するでしょう。__

この地図は、現実的なデザイン戦略の基礎になりうるものです。

次のページでは、関係の特徴付けをより具体的にし、境界のある文脈間の関係のコモンパターンのセットを示します。

### Partnership *

2つのコンテキストで共にチームが成功または失敗すると、協力的な関係が頻繁に出現します。

Poor coordination of mutually dependent subsystems in separate contexts leads to delivery failure for both projects. A key feature missing from one system might make the other system undeliverable. Interfaces that do not match the expectations of the developers of the other subsystem could cause integration to fail. A mutually agreed interface might turn out to be so awkward to use that it slows the development of the client system, or so difficult to implement that it slows the development of the server subsystem. Failure brings both projects down.

Therefore:

__Where development failure in either of two contexts would result in delivery failure for both, forge a partnership between the teams in charge of the two contexts. Institute a process for coordinated planning of development and joint management of integration.__

__The teams must cooperate on the evolution of their interfaces to accommodate the development needs of both systems. Interdependent features should be scheduled so that they are completed for the same release.__

It is not necessary, most of the time, for developers to understand the model of the other subsystem in detail, but they must coordinate their project planning. When development in one context hits obstacles, then joint examination of the issue is called for, to find an expeditious design solution that does not overly compromise either context.

Also, a clear process is needed to govern integration. For example, a special test suite can be defined that proves the interface meets the expectations of the client system, which can be run as part of continuous integration on the server system.

### Shared Kernel

_モデルの一部が関連するコードと共有されていると非常に密接な相互依存関係にあり、設計作業に影響を与えたり、それをひそかに傷つける可能性があります。_

機能統合が制限されている場合、大規模コンテキストの継続的統合のオーバーヘッドは高すぎると見なされる可能性があります。 これは、チームが継続的な統合を維持するためのスキルや政治組織を持っていない場合、または単一のチームが大きすぎて扱いにくい場合に特に当てはまります。 そのため、境界のあるコンテキストを別々に定義し、複数のチームを結成しましょう。

密接に関連したアプリケーションに取り組んでいる別々の、調整されていないチームはしばらくの間レースを進めることができますが、彼らが作り出すものは噛み合わないかもしれません。 パートナーチームでさえ、翻訳レイヤと後付けに多大な時間を費やすことになり、その間に努力が重複し、一般的なユビキタス言語の利点を失う可能性があります。

Therefore:

__チームがすすんで共有するようなドメインモデルのサブセットを明示的な境界で指定します。 このカーネルを小さくしてください。__

__この境界内に、モデルのこのサブセットとともに、モデルのその部分に関連するコードまたはデータベース設計のサブセットを含めます。 この明示的に共有されたものには特別な地位があり、他のチームと相談しないで変更するべきではありません。__

カーネルモデルを厳密に保ち、チームのユビキタス言語を調整する継続的な統合プロセスを定義します。 機能システムを頻繁に統合しますが、チーム内での継続的統合のペースよりはやや少ないです。

### Customer/Supplier Development

_2つのチームがアップストリームとダウンストリームの関係にあり、アップストリームのチームがダウンストリームのチームの運命とは無関係に成功する可能性がある場合、ダウンストリームのニーズはさまざまな方法で対処されるようになります。_

ダウンストリームのチームは、アップストリームが優先されるために無力化されることがあります。 つまり、アップストリームのチームは抑制されるかもしれず、ダウンストリームのシステムを壊すことを心配します。 ダウンストリームチームの問題は、複雑な承認プロセスを伴う面倒な変更依頼手順によっては改善されません。また、 ダウンストリームチームが変更に対する拒否権を持っている場合、アップストリームチームの自由な開発は阻止されます。

Therefore:

__2つのチームの間に明確なカスタマー／サプライヤの関係を確立します。これは、下流の優先順位が上流の計画に組み込まれることを意味します。 全員がコミットメントとスケジュールを理解できるように、下流の要件についてタスクを交渉し予算を組みます。__

アジャイルチームは、計画セッションにおいて、下流チームが上流チームに対してカスタマーの役割を果たすようにできます。 共同開発された自動受け入れテストは、上流から期待されるインタフェースを検証することができます。 これらのテストをアップストリームチームのテストスイートに追加し、継続的な統合の一環として実行することで、ダウンストリームの副作用を心配せずにアップストリームチームが変更を加えることができます。

### Conformist

2つの開発チームが、上流チームが下流チームのニーズを満たす動機を持たない上流/下流関係にある場合、下流チームは無力です。 利他主義は上流の開発者が約束をするように動機付けるかもしれませんが、それらが実現されることはまずありません。 これらの善意を信じることで、川下のチームは利用できなくなる機能に基づいて計画を立てるようになります。 下流のプロジェクトは、チームが最終的にそれが与えられたものを我慢して受け入れて学ぶまで遅れるでしょう。 下流チームのニーズに合わせたインターフェースはカードにはありません。

Therefore:

__上流チームのモデルに忠実に従うことで、境界のあるコンテキスト間の翻訳の複雑さを排除します。 これは下流の設計者のスタイルを悩ませ、おそらくアプリケーションにとって理想的なモデルを生み出さないでしょうが、適合性を選択することは統合を非常に単純化します。 また、上流のチームとユビキタス言語を共有します。 上流は運転席にあるので、彼らにとってコミュニケーションを容易にするのは良いことです。 利他主義は、彼らにあなたと情報を共有させるのに十分かもしれません。__

### Anticorruption Layer

うまく設計された境界のあるコンテキストを協調的なチームと橋渡しするとき、翻訳レイヤは単純でエレガントなものになることがあります。 しかし、制御やコミュニケーションが、共有されたカーネル、パートナー、あるいはカスタマー/サプライヤの関係をやめるのに十分でない場合、翻訳はより複雑になります。 翻訳レイヤはより防御的なトーンを帯びます。

A large interface with an upstream system can eventually overwhelm the intent of the downstream model altogether, causing it to be modified to resemble the other system’s model in an ad hoc fashion. The models of legacy systems are usually weak (if not big balls of mud), and even the exception that is clearly designed may not fit the needs of the current project, making it impractical to conform to the upstream model. Yet the integration may be very valuable or even required for the downstream project.

Therefore:

__As a downstream client, create an isolating layer to provide your system with functionality of the upstream system in terms of your own domain model. This layer talks to the other system through its existing interface, requiring little or no modification to the other system. Internally, the layer translates in one or both directions as necessary between the two models.__

### Open-host Service

Typically for each bounded context, you will define a translation layer for each component with which you have to integrate that is outside the context. Where integration is one-off, this approach of inserting a translation layer for each external system avoids corruption of the models with a minimum of cost. But when you find your subsystem in high demand, you may need a more flexible approach.

When a subsystem has to be integrated with many others, customizing a translator for each can bog down the team. There is more and more to maintain, and more and more to worry about when changes are made.

Therefore:

__Define a protocol that gives access to your subsystem as a set of services. Open the protocol so that all who need to integrate with you can use it. Enhance and expand the protocol to handle new integration requirements, except when a single team has idiosyncratic needs. Then, use a one-off translator to augment the protocol for that special case so that the shared protocol can stay simple and coherent.__

This places the provider of the service in the upstream position. Each client is downstream, and typically some of them will be conformist and some will build anticorruption layers. A context with an open host service might have any sort of relationship to contexts other than its clients.

### Published Language

_The translation between the models of two bounded contexts requires a common language._

Direct translation to and from the existing domain models may not be a good solution. Those models may be overly complex or poorly factored. They are probably undocumented. If one is used as a data interchange language, it essentially becomes frozen and cannot respond to new development needs.

Therefore:

__Use a well-documented shared language that can express the necessary domain information as a common medium of communication, translating as necessary into and out of that language.__

Many industries establish published languages in the form of data interchange standards. Project teams also develop their own for use within their organization.

Published language is often combined with open-host service.

### Separate Ways

We must be ruthless when it comes to defining requirements. If two sets of functionality have no significant relationship, they can be completely cut loose from each other.

Integration is always expensive, and sometimes the benefit is small.

Therefore:

__Declare a bounded context to have no connection to the others at all, allowing developers to find simple, specialized solutions within this small scope.__

### Big Ball of Mud *

As we survey existing software systems, trying to understand how distinct models are being applied within defined boundaries, we find parts of systems, often large ones, where models are mixed and boundaries are inconsistent.

It is easy to get bogged down in an attempt to describe the context boundaries of models in systems where there simply are no boundaries.

Well-defined context boundaries only emerge as a result of intellectual choices and social forces (even though the people creating the systems may not always have been consciously aware of these causes at the time). When these factors are absent, or disappear, multiple conceptual systems and mix together, making definitions and rules ambiguous or contradictory. The systems are made to work by contingent logic as features are added. Dependencies crisscross the software. Cause and effect become more and more difficult to trace. Eventually the software congeals into a big ball of mud.

The big ball of mud is actually quite practical for some situations (as described in the original article by Foote and Yoder), but it almost completely prevents the subtlety and precision needed for useful models.

Therefore:

__Draw a boundary around the entire mess and designate it a big ball of mud. Do not try to apply sophisticated modeling within this context. Be alert to the tendency for such systems to sprawl into other contexts.__

(see http://www.laputan.org/mud/mud.html. Brian Foote and Joseph Yoder)
