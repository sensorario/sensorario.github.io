---
layout: post
title:  "Value Objects"
date:   2015-06-22
categories: ddd
---

<style type="text/css">
<!--
pre { white-space: pre-wrap; font-family: monospace; color: #ffffff; background-color: #000000; }
body { font-family: monospace; color: #ffffff; background-color: #000000; }
.lnr { color: #804000; }
.Constant { color: #af5f00; }
.Identifier { color: #008080; font-weight: bold; }
.Statement { color: #804000; }
.PreProc { color: #c000c0; }
.Comment { color: #008080; }
.Special { color: #c000c0; }
.Type { color: #008000; }
-->
</style>

<div class="introduction">
    <em>If we are talking about Value Objects, we are inside a specific context: Domainr-Driven Design. And What is Domain Driven Design? Is a way to produce quality in the software we develop. Some quality is reached by using tests avoiding delivering software with fatal number of bugs. Quality of software is reached via tests. Wuality of design could be reached with Domain-Driven Design. DDD gives you tools necessary to high-quality software. Value Objects are a vital building block of DDD.</em>

    <h2>What is a Value Object</h2>
    <p>Value Objects are Value Types that measures, quantify, or describe things. It's just a bundle ov values that comes and goes as needed. When designed correctly, a Value instance can be created, handed off, and forgotten about. A value object could be ...</p>
    <ul>
        <li>numbers</li>
        <li>text strings</li>
        <li>dates</li>
        <li>times</li>
        <li>person's full name</li>
        <li>currecy</li>
        <li>color</li>
        <li>phone number</li>
        <li>postal addresses</li>
        <li>email address</li>
        <li>json</li>
        <li>uri</li>
        <li>url</li>
        <li>...</li>
        <li>an event</li>
        <li>http message</li>
        <li>http status code</li>
    </ul>

    <h2>Ubiquitous Language</h2>
    <p>Is a shared team language. It's shared by domain experts and developers. In fact, it's shared by everyone on the project team. No matter your role on the team, since you are on the team you use the Ubiquitous Language of the project. Is not an adoption of business language. Is not industry standard. Is a language developed by the team, composed of both domain experts and software developers.</p>

    <h2>How do we determine if a domain concept should be modeled as a Value?</h2>
    <p>To answer, we need to pay attention to its characteristics. When you care only about the attributes of an element of the model, classify it as a Value Object. Treat the Value Object as immutable. Don't give it any identity and avoid the design complexities necessary to mantain Entities.</p>
    <p>If we are interested of a value and not about an identity, we need a value object. Is ONE sum of values that an entity can assume. A value object, could be equals to more entities. And more entities could be equals to one value object.</p>
</div>

<div class="characteristics">
    <h2>Characteristics</h2>
    <p>When you are trying to decide if a concept is a Value, you should determine whether it possesses most of these characteristics:</p>
    <ul>
        <li>measures, quantifies, or describes a thing in the domain</li>
        <li><a href="#immutable">immutable</a></li>
        <li>conceptual whole</li>
        <li>replaceable</li>
        <li>equality</li>
        <li>Side-Effect-Free</li>
    </ul>
</div>

<div class="measures">
    <h2>Measures, Quantifies or Describes</h2>
    <p>A Value Object is not a thing of our domain. A person has an age. Age is not a thing. Age measures an amount of years. A person has a name. The name is not a thing. Name describes how the person is called. Name is a description? Name is a Value Object.</p>
</div>

<div class="immutability">
    <a name="immutable"></a>
    <h2>Immutable</h2>
    <p>This means that Value Object are stateless. We cannot modify a value object. Setters violate immutability.</p>
    <p>In some implementation, in other languages, setters are allowed BUT with private visiblity. In these cases basic attribute initialization is oerfirned first by invoking basic private setters.</p>
    <p>You can design a Value Object handled to one or more Entities. But is not a good idea because if Entity change, Value changes too, and this is a violation of the quality of immutability. State cannot change! Is Value Object you have disigned need state changement, consider the idea to use an Entity.</p>
    <pre>
    <span class="lnr"> 2 </span><span class="Type">namespace</span> Sensorario\PugMi\ValueObjects;
    <span class="lnr"> 3 </span>
    <span class="lnr"> 4 </span><span class="Type">final</span> <span class="Type">class</span> EmailAddress <span class="Special">{</span>
    <span class="lnr"> 5 </span>    <span class="Comment">// we need a public constructor?</span>
    <span class="lnr"> 6 </span>    <span class="Type">private</span> <span class="PreProc">function</span> <span class="Statement">__construct</span><span class="Special">()</span> <span class="Special">{</span>
    <span class="lnr"> 7 </span>        <span class="Comment">// ...</span>
    <span class="lnr"> 8 </span>    <span class="Special">}</span>
    <span class="lnr"> 9 </span>    <span class="Comment">// named constructor</span>
    <span class="lnr">10 </span>    <span class="Type">public</span> <span class="Type">static</span> <span class="PreProc">function</span> withDomain<span class="Special">(</span><span class="Statement">$</span><span class="Identifier">domain</span><span class="Special">)</span> <span class="Special">{</span>
    <span class="lnr">11 </span>        <span class="Statement">return</span> <span class="PreProc">new</span> <span class="Type">self</span><span class="Special">(</span><span class="Statement">compact</span><span class="Special">(</span>'<span class="Constant">domain</span>'<span class="Special">))</span>;
    <span class="lnr">12 </span>    <span class="Special">}</span>
    <span class="lnr">13 </span>    <span class="Comment">// named constructor</span>
    <span class="lnr">14 </span>    <span class="Type">public</span> <span class="Type">static</span> <span class="PreProc">function</span> withAddress<span class="Special">(</span><span class="Statement">$</span><span class="Identifier">address</span><span class="Special">)</span> <span class="Special">{</span>
    <span class="lnr">15 </span>        <span class="Statement">return</span> <span class="PreProc">new</span> <span class="Type">self</span><span class="Special">(</span><span class="Statement">compact</span><span class="Special">(</span>'<span class="Constant">address</span>'<span class="Special">))</span>;
    <span class="lnr">16 </span>    <span class="Special">}</span>
    <span class="lnr">17 </span><span class="Special">}</span>
    </pre>
</div>

<div class="immutability">
    <h2>Conceptual Whole</h2>
    <p>Only toghether, the one, two or a number of individual attributes, form the complete intended measure or description.</p>
    <p>"50/EUR" contains two attributes: "50" and "EUR". Separately these attributes describes something else or nothing special. These attributes are a <strong>Conceptual Whole</strong> that describe a monetary measure. What we care about is not just an amount or just a currency. To properly describe a thing, it must be trated not as two separate attributes, but as a whole value.</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;

        public final class MonetaryMeasure {
            public static function withAmountAndCurrency($amount, $currency) {
                return new self(compact(
                    'amount',
                    'currency'
                ));
            }
        }
    </code>
    <p>Each attribute (necessary) is defined! A Value Object is a sort of defined state. A Value Object is a container of attributes.</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;
        $person = new Person();
        $person->name('Simone');
        $person->company('Onebip');
    </code>
    <p>The name of attributes must reflect this characteristic.</p>
    <code>
        MonetaryMeasure::withAmountAndCurrency(50, "EUR");
    </code>
    <!--<p>This is not perfect. We can use additiona type such as Currency. Or Amount.</p>
    <code>
        namespace Sensorario\Pug\ValueObjects;
        public final class MonetaryMeasure {
            public static function withAmountAndCurrency(Amount $amount, Currency $currency) {
                return new self([
                    "amount"   => $amount->value(),
                    "currency" => (string) $currency,
                ]);
            }
        }
    </code>
    <p>This makes VO more descriptive. And a Factory and possibly a Builder, can take care about VO creation.</p>
    <p>We can user other value object, to define a value object. In this case, the parent reference to a Value Object is not just an attribute. Rather, it is a property of the containing parent in the model that holds a reference to it. Also, ... in this case, names of attributes can be determined only after establishing our Bounded Context and its Ubiquitous Language.</p>
    <p>Use of plain string can cause problems. Defining a ThingName type instead, we can centralize all concerns dealing with the name of a ThingOfWorth.</p> -->
</div>

<div class="immutability">
    <h2>Replaceabiliy</h2>
    <p>When an entire value is replaced, and still represent the currently correct whole.</p>
    <p>3 is a number. 42 is a number. 42 could completely replace 3. Che conceptual whole is "the answer". We'll not alter 3 value. We change total value to 42.</p>
    <code>
        namespace Sensorario\Pug\ValueObjects;

        $answer = 3;
        $answer = 42;
    </code>
    <p>We have replaced the entire value. This is the point of Value Objects. The point of replacement. Is not an oversemplification. It is exactly what replacement does even when Value Object type is more complex than an integer.</p>
    <code>
        namespace Sensorario\Pug\ValueObjects;

        $amount = "3/EUR";
        $amount = "4/EUR";
        $amount = "3/USD";
        $amount = "42/EUR";
    </code>
    <code>
        namespace Sensorario\Pug\ValueObjects;
        $fullName = FullName::fromSurnameName("Gentili", "Simone");
        $fullName = FullName::fromSurameNickAndName("Gentili", "Demo", "Simone");

        $fullName = FullName::box([
            'surname' => "Gentili",
            'name'    => "Simone",
        ]);

        $fullName = FullName::box([
            'surname'  => "Gentili",
            'nickname' => "Demo",
            'name'     => "Simone",
        ]);
    </code>
    <p>Use a method to change the state of che concept "full name" should violate the immutability. Instead of change the value, we replace the previous fill name with the noew one. An entity should use our new Value Object to set the full name of Person class.</p>
    <p>Replacement is not practical. But replacement also responds to another characteristics of Value Objects: Side-Effect-Free Behavior. Each time we make some operation with a value object, if the kind (the class) is the same, the instance is totally renewed.</p>
</div>

<div class="immutability">
    <h2>Equality</h2>
    <p>If both types and their attributes are equal, the Value are considered equal. Further, if any two or more Value instances are equal, you could assign any one of the equal Value instances to an Entity's property  and the assignment would not change the value of the property.</p>
    <p>Ask yourself if the concept you are designing must be an Entity identified uniqeuely from all other object or if it sufficiently supported using value equality. If the consept itself doesnt require unique identity, model it as a Value Object.</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;

        $a = new Currency('USD');
        $b = new Currency('USD');

        var_dump($a == $b);  // bool(true)
        var_dump($a === $b); // bool(false)

        $c = new Currency('EUR');

        var_dump($a == $c);  // bool(false)
        var_dump($a === $c); // bool(false)
    </code>
    <!-- add here image of liuggio tweets -->
</div>

<div class="immutability">
    <h2>Side-Effect-Free Behavior</h2>
    <p>"Since no modification occurs when executing a specific operation, that operation is said to be side-effect free." All methods of a Value Objects are side-effect free, because they must not violate the immutability characteristics. We might see Value Objects only as attribute container</p>
    <p>Pure functional programming languages allow nothing but side-effect-free behavior, requiring all closures to receive and produce only immutable value objects.</p>
    <code>
        namespace Sensorario\Pug\ValueObjects;

        $fullName = new FullName("Gentili", "Simone");
        $fullName->withNickname("Demo"); // modifiche perse
        $fullName = $fullName->withNickname("Demo");
    </code>
    <p>The method withNickname() must respect the side-effect-free rule. Value Objects are immutable. Thus, the method will generate new container of attributes. Thw use of methods withSomething(), make all more expressive. The method will be implemented in this way:</p>
    <code>
        namespace Sensorario\Pug\ValueObjects;

        class FullName {
            private function __construct(array $params = []) {
                // ...
            }
            public static function withNickname($nickname) {
                return new self([
                    'name' => $this->name(),
                    'surname' => $this->name(),
                    'nickname' => $nickname,
                ]);
            }
        }
    </code>
    <p>Method must not modify the state. Every function will generate new value.</p>
    <p>This method also capture important business logic.</p>
    <p>When we pass an entity as a function parameter, we must not modify that entity. Why? the side-effect free does not regard only Value Object: it also regard the other domain parts. If we need to change the state of the entity, function can take the entity as input and return something the entity could use to modify itself, on its own terms and responsibility.</p>
</div>

<div class="standard-types">
    <p>Standard Types are descriptive obejects that indicates the type of things. Synonimous od standard type are called <em>type code</em> or <em>lookup</em>. PhoneNumber is a value. But phone number hide an information about the type. We need to describe it as personal number or work number. These descriptions represent standard type.</p>
    <p>In case of currency, standard types could be EUR, USD, ... and so on. Using a standard type helps avoid bogus currencies. Use a Value Object helps development avoiding bogus in values.</p>
    <p>Depending on the level of standardisation: type could be defined in a txt file, exel, ... OR accepted as international standards.</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;

        final class HTTPStatusCodes {
            const OK        = 200;
            const NOT_FOUND = 404;
        }
    </code>
</div>

<div class="testing-value-objects">
    <p>There are several way to test code. To test a single class, we have unit tests. To test a group of object collaboration, we have functional tests. At the end, to test the whole application, we have end-to-end tests.</p>
    <p>In functional tests, we use to mock collaborators. But what happens during a functional test, where collaborator is a Value Object? Need we to mock its behavior? I dont think: because of Value Objects characteristics, we dont (IMHO). Value objects, returns alwais same results. Two value objects are equals if their values are equals.</p>
    <p>There is no reasons to mock a value object. Value objects, are immutable so just create new instance and use it. Value object is a container of values.</p>
    <p>Value cannot change their state. So, 42 is always 42. 21 May 2015 is always 21 May 2015. So we cant mock a value. It is easier and less error prone, to use a real type. A value should be so simple that there is no benefit to mock them. Mock objects, aims to mime real objects.</p>
</div>

<div class="final-classes">
    <p>Now let's talk about open/closed principle. The principle says "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification". "Closed for modification, in this context, means that when your code exposes some behavior to the outside world, that interface should be stable. Providing an API is a responsibility: by allowing other code to access features of your system, you need to give certain guarantees of stability or low change frequency. The behaviour should be deterministic. It does not mean your implementation can not change. The changes should not affect outside code.". If a method is private, is removable. If an element is needed only inside an'object, is removable. Hidden attributes, behaviors and methods, ... are removable and closed to change. Nothing depends on it and. "Somewhere, perhaps invisible to you, something might depend on it. Closing it, or even making a small change, will break that code."</p>
</div>

<div class="implementation">
    <p>If all setter has private scope, there is no opportunity for attributes to be exposed to mutation by consumers.</p>
    <p>Fluent interface!</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;

        $valueObject = ValueObject::box([
            'attribute' => 'value',
        ]);

        $request = Request::withCode(200);
        $request = $request->andHeader('Referer', 'http://sensorario.github.io');
    </code>
    <p>Value Objects and encapsulation. Mmmm. "Functions should have a small number of arguments. No argument is best, followed by one, two, and three. More than three is very questionable and should be avoided with prejudice." But, what hannpes when we need more and more third party class in a static method of our value object? My question is, ... How many third party elements can I accept, and still think this object as a Value Objecr?</p>
    <code>
        namespace Sensorario\PugMi\ValueObjects;

        use Sensorario\Stuff;

        class MyValueObject
        {
            public static function withEncapsulation()
            {
                $foo = new Stuff('foo');
                return new self(compact('foo'));
            }
        }
    </code>
    <p>Whatching Value Objects characteristics, ... this class measures, is immutable, conceptual whole, is replaceable, respect equality and has side-effect-free. This characteristics are respected only if Stuff class has static behavior. Remember that for immutability, if a Value Object is related to an entity and the entity change, also Value Object changes. If this happens, you have not a Value Object in your hand.</p>
</div>

<div class="persisting-value-object">
    <p>There are a variety of ways to persit Value Object instances to a persistent store. We are interested in persisting Values along with the state of the aggregate instances that contain them. These examples are based on the assumpion that an Aggregate is beign added to or read from its Repository, and its contained Values are persisted and reconstituted behind the scenes along with the Entity that contains them.</p>
    <p>ORM such Doctrine2 is popular and widely used. Using an ORM to map every class to a table and every attribute to a column adds complexity, which may be unwarranted.</p>
    <p>Most times that a Value Object is persisted to a data store, it is stored in a denormalized fashion. Its attributes are stored in the same database table row as its Entity object. This makes the storage and retrieval of Values clean and optimized and prevents any persistence store leakage into the model. It's both a pleasure and a relief when Values can be persisted this way.</p>
    <p>There are times when Value Objects in the model will of necessary be stored as an Entity with respect to a relational persistence store. When persisted an instance of a specific value object type will occupy its own row in a relational database table that exists specifically for its own row in a relational database table that exists specifically for its type, and it will have its own database primary key column. This happens when, when supporting a collection of Value Object instance with ORM. In such cases the Value type persistent data is modeled as a database entity.</p>
    <p>Is this an indication that the domain model object should reflect the design of the data model and be an Entity rather.</p>
    <p>Persisting a single Value Object instance to a database is straightforward. </p>
</div>

<div class="resources">
    <h1>Interesting Github repositories</h1>
    <ul>
        <li><a href="https://github.com/nicolopignatelli/valueobjects">nicolopignatelli/valueobjects</a></li>
        <li><a href="https://github.com/satooshi/ValueObject">satooshi/ValueObject</a></li>
    </ul>

    <h1>Suggested Books</h1>
    <ul>
        <li><a href="https://leanpub.com/ddd-in-php">ddd in php</a></li>
        <li><a href="http://www.amazon.it/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882">Clean code</a></li>
    </ul>

    <h2>Links</h2>
    <ul>
        <li><a hreg="http://verraes.net/2014/05/final-classes-in-php/">final classes in php</a></li>
        <li><a href="http://martinfowler.com/bliki/ValueObject.html">Value object (Martin Fowler)</a></li>
        <li><a href="http://css.dzone.com/articles/unit-testing-when-value">unit test when value</a></li>
        <li><a href="http://verraes.net/2014/06/named-constructors-in-php/">named constructor</a></li>
        <li><a href="http://www.mockobjects.com/2007/04/test-smell-everything-is-mocked.html">don't mock value objects</a></li>
    </ul>
</div>
