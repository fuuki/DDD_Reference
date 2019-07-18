## II. Building Blocks of a Model-Driven Design

これらのパターンは、ドメイン駆動設計を踏まえて、広く保持されているオブジェクト指向設計のベストプラクティスをキャストします。彼らは、モデルを明確にし、モデルと実装を互いに整合させ、互いの効果を強化するための決定を導きます。個々のモデル要素の詳細を慎重に作成することで、開発者はモデルを探索し、それらを実装と密接に対応させるための安定したプラットフォームを得ることができます。

### Layered Architecture

オブジェクト指向プログラムでは、UI、データベース、およびその他のサポートコードは、多くの場合、ビジネスオブジェクトに直接書き込まれます。 追加のビジネスロジックは、UIウィジェットおよびデータベーススクリプトの動作に組み込まれています。 このような方法は、短期的には、プログラムを動作させるのに最も簡単であるために行われます。

このような大量の他のコードを介してドメイン関連のコードが散乱すると、見辛く、解析が非常に困難になります。 UIに対する表面的な変更は、実際にはビジネスロジックを変更している可能性があります。ビジネスルールを変更するには、UIコード、データベースコード、またはその他のプログラム要素を綿密にトレースする必要があります。コヒーレントでモデル駆動型のオブジェクトを実装することは現実的ではありません。自動テストが扱いにくくなります。それぞれの活動に関わるすべての技術と論理で、プログラムは非常に単純に保たれなければならなりません。さもなければ、理解するのが不可能になります。

Therefore:

__ドメインモデルとビジネスロジックの表現を分離し、ビジネスロジックではないインフラストラクチャ、ユーザーインターフェイス、アプリケーションロジックへの依存を排除しましょう。複雑なプログラムを複数の層に分割します。各レイヤーは、レイヤーの中でまとまりがあり、下のレイヤーにのみ依存する設計にしましょう。 スタンダードなアーキテクチャパターンに従って、上の層との疎結合を実現します。ドメインモデルに関連するすべてのコードを単一の層に集中させ、それをユーザーインターフェイス、アプリケーション、およびインフラストラクチャコードから分離します。ドメインオブジェクトは、自分自身の表示、自分自身の保存、アプリケーションタスクの管理などの責任を負うことなく、ドメインモデルの表現に集中できます。これにより、モデルを進化させて、不可欠なビジネス知識を捉え、それを機能させるのに十分なほどリッチで明確なものにすることができます。__

ここでキーとなるゴールは隔絶です。「Hexagonal Architecture」などの関連するパターンは、ドメインモデル表現が、システムの他の部分への依存や参照を避けるのはもちろん、それ以上に役立つことがあります。

### Entities

多くのオブジェクトは、ライフサイクルを経て、継続性と同一性のスレッドを表しますが、それらの属性は変わる可能性があります。

ときに、主にオブジェクトを定義づけるのは、その属性ではありません。それらは時間の中を経て、しばしば異なる表現を横切って走る、同一識別子のスレッドを表します。属性が異なっていても、そのようなオブジェクトは別のオブジェクトと一致しなければならないことがあります。オブジェクトは同じ属性を持っていても他のオブジェクトと区別されなければなりません。誤ったIDを使用すると、データが破損する可能性があります。

Therefore:

__オブジェクトが、その属性ではなく、その識別子によって区別される場合は、これをモデル内のその定義の中心にします。 クラス定義を単純にし、ライフサイクルの継続性と識別子に焦点を当てます。__

__形や履歴に関係なく、各オブジェクトを区別する方法を定義しましょう。 属性によってオブジェクトを一致させることを要求する要件に注意してください。 一意であることが保証されているシンボルを添付することによって、各オブジェクトに対して一意の結果が得られることが保証されている操作を定義します。 この識別手段は、外部から来る場合もあれば、システムによって作成されシステムに対して作成される任意の識別子である場合もありますが、モデル内のIDの区別に対応している必要があります。__

__モデルは、それが意味するものが常に同じになるように定義しなければなりません。__

(aka Reference Objects)

### Value Objects

いくつかのオブジェクトは物のいくつかの特性を記述または計算します。

多くのオブジェクトは概念的なアイデンティティを持ちません。

エンティティの識別情報を追跡することは不可欠ですが、他のオブジェクトに識別情報を添付すると、システムパフォーマンスが低下し、分析作業が追加され、すべてのオブジェクトを同じように見せることでモデルが混乱する可能性があります。 ソフトウェア設計は複雑さを伴う絶え間ない戦いです。 特別な取り扱いが必要な場合にのみ適用されるように、私たちは区別をしなければなりません。

ただし、このカテゴリのオブジェクトを単なる識別子の欠如と見なすと、ツールボックスや語彙に多くの情報が追加されません。 実際、これらのオブジェクトは、それぞれ独自の特性、およびモデルに対する独自の意味を持っています。 これらは物事を説明するオブジェクトです。

Therefore:

__モデルの要素の属性とロジックだけを気にする場合は、値オブジェクトとして分類してください。 それが伝える属性の意味を表現し、それに関連する機能を与えるようにします。 値オブジェクトを不変として扱います。 すべての操作は、変更可能なステートに依存しない、副作用のない関数にします。 値オブジェクトに識別子を与えず、エンティティを維持するのに必要な設計の複雑さを避けてください。__

### Domain Events *

ドメインエキスパートが気にかけていることが起こりました。

An entity is responsible for tracking its state and the rules regulating its lifecycle. But if you need to know the actual causes of the state changes, this is typically not explicit, and it may be difficult to explain how the system got the way it is. Audit trails can allow tracing, but are not usually suited to being used for the logic of the program itself. Change histories of entities can allow access to previous states, but ignores the meaning of those changes, so that any manipulation of the information is procedural, and often pushed out of the domain layer.

A distinct, though related set of issues arises in distributed systems. The state of a distributed system cannot be kept completely consistent at all times. We keep the aggregates internally consistent at all times, while making other changes asynchronously. As changes propagate across nodes of a network, it can be difficult to resolve multiple updates arriving out of order or from distinct sources.

Therefore:

__Model information about activity in the domain as a series of discrete events. Represent each event as a domain object. These are distinct from system events that reflect activity within the software itself, although often a system event is associated with a domain event, either as part of a response to the domain event or as a way of carrying information about the domain event into the system.__

__A domain event is a full-fledged part of the domain model, a representation of something that happened in the domain. Ignore irrelevant domain activity while making explicit the events that the domain experts want to track or be notified of, or which are associated with state change in the other model objects.__

In a distributed system, the state of an entity can be inferred from the domain events currently known to a particular node, allowing a coherent model in the absence of full information about the system as a whole.

Domain events are ordinarily immutable, as they are a record of something in the past. In addition to a description of the event, a domain event typically contains a timestamp for the time the event occurred and the identity of entities involved in the event. Also, a domain event often has a separate timestamp indicating when the event was entered into the system and the identity of the person who entered it. When useful, an identity for the domain event can be based on some set of these properties. So, for example, if two instances of the same event arrive at a node they can be recognized as the same.

### Services

Sometimes, it just isn’t a thing.
Some concepts from the domain aren’t natural to model as objects. Forcing the required domain functionality to be the responsibility of an entity or value either distorts the definition of a model-based object or adds meaningless artificial objects.

Therefore:

__When a significant process or transformation in the domain is not a natural responsibility of an entity or value object, add an operation to the model as a standalone interface declared as a service. Define a service contract, a set of assertions about interactions with the service. (See assertions.) State these assertions in the ubiquitous language of a specific bounded context. Give the service a name, which also becomes part of the ubiquitous language.__

### Modules

Everyone uses modules, but few treat them as a full-fledged part of the model. Code gets broken down into all sorts of categories, from aspects of the technical architecture to developers’ work assignments. Even developers who refactor a lot tend to content themselves with modules conceived early in the project.
Explanations of coupling and cohesion tend to make them sound like technical metrics, to be judged mechanically based on the distributions of associations and interactions. Yet it isn’t just code being divided into modules, but also concepts. There is a limit to how many things a person can think about at once (hence low coupling). Incoherent fragments of ideas are as hard to understand as an undifferentiated soup of ideas (hence high cohesion).

Therefore:

__Choose modules that tell the story of the system and contain a cohesive set of concepts. Give the modules names that become part of the ubiquitous language. Modules are part of the model and their names should reflect insight into the domain.__

__This often yields low coupling between modules, but if it doesn’t look for a way to change the model to disentangle the concepts, or an overlooked concept that might be the basis of a module that would bring the elements together in a meaningful way. Seek low coupling in the sense of concepts that can be understood and reasoned about independently. Refine the model until it partitions according to high-level domain concepts and the corresponding code is decoupled as well.__

(aka Packages)

### Aggregates

It is difficult to guarantee the consistency of changes to objects in a model with complex associations. Objects are supposed to maintain their own internal consistent state, but they can be blindsided by changes in other objects that are conceptually constituent parts. Cautious database locking schemes cause multiple users to interfere pointlessly with each other and can make a system unusable. Similar issues arise when distributing objects among multiple servers, or designing asynchronous transactions.

Therefore:

__Cluster the entities and value objects into aggregates and define boundaries around each. Choose one entity to be the root of each aggregate, and allow external objects to hold references to the root only (references to internal members passed out for use within a single operation only). Define properties and invariants for the aggregate as a whole and give enforcement responsibility to the root or some designated framework mechanism.__

Use the same aggregate boundaries to govern transactions and distribution.

Within an aggregate boundary, apply consistency rules synchronously. Across boundaries, handle updates asynchronously.

Keep an aggregate together on one server. Allow different aggregates to be distributed among nodes.

When these design decisions are not being guided well by the aggregate boundaries, reconsider the model. Is the domain scenario hinting at an important new insight? Such changes often improve the model’s expressiveness and flexibility as well as resolving the transactional and distributional issues.

### Repositories

_Query access to aggregates expressed in the ubiquitous language._

Proliferation of traversable associations used only for finding things muddles the model. In mature models, queries often express domain concepts. Yet queries can cause problems.

The sheer technical complexity of applying most database access infrastructure quickly swamps the client code, which leads developers to dumb-down the domain layer, which makes the model irrelevant.

A query framework may encapsulate most of that technical complexity, enabling developers to pull the exact data they need from the database in a more automated or declarative way, but that only solves part of the problem.

Unconstrained queries may pull specific fields from objects, breaching encapsulation, or instantiate a few specific objects from the interior of an aggregate, blindsiding the aggregate root and making it impossible for these objects to enforce the rules of the domain model. Domain logic moves into queries and application layer code, and the entities and value objects become mere data containers.

Therefore:

__For each type of aggregate that needs global access, create a service that can provide the illusion of an in-memory collection of all objects of that aggregate’s root type. Set up access through a well-known global interface. Provide methods to add and remove objects, which will encapsulate the actual insertion or removal of data in the data store. Provide methods that select objects based on criteria meaningful to domain experts. Return fully instantiated objects or collections of objects whose attribute values meet the criteria, thereby encapsulating the actual storage and query technology, or return proxies that give the illusion of fully instantiated aggregates in a lazy way. Provide repositories only for aggregate roots that actually need direct access. Keep application logic focused on the model, delegating all object storage and access to the repositories.__

### Factories

When creation of an entire, internally consistent aggregate, or a large value object, becomes complicated or reveals too much of the internal structure, factories provide encapsulation.
Creation of an object can be a major operation in itself, but complex assembly operations do not fit the responsibility of the created objects. Combining such responsibilities can produce ungainly designs that are hard to understand. Making the client direct construction muddies the design of the client, breaches encapsulation of the assembled object or aggregate, and overly couples the client to the implementation of the created object.

Therefore:

__Shift the responsibility for creating instances of complex objects and aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create an entire aggregate as a piece, enforcing its invariants. Create a complex value object as a piece, possibly after assembling the elements with a builder.__
