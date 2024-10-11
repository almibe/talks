<script lang="ts">
import { browser } from '$app/environment';

import Reveal from 'reveal.js';

import "reveal.js/dist/reveal.css"

if (browser) {

    let deck = new Reveal({
    })
    deck.initialize()
}
</script>

<div class="reveal">
    <div class="slides">
        <section>
            <section>
                <h1>An Introduction to Description Logic</h1>
                <img alt="Description Logic Logo" src="/dl-small.gif" />
                <img alt="Description Logic Logo" src="/dl2-small.gif" />
                <img alt="Description Logic Logo" src="/dl-small.gif" />
                <h2>Alex Michael Berry</h2>
                <p><a href="https://almibe.dev">almibe.dev</a></p>
                <p><a href="https://github.com/almibe/talks">github.com/almibe/talks</a></p>
                <p>Logos from <a href="https://dl.kr.org/logo.html">https://dl.kr.org/logo.html</a>, made by Enrico Franconi and Sebastian Brandt</p>
            </section>
            <section>
                <h1>Overview</h1>
                <h2>Background & History</h2>
                <h2>An Introduction to Description Logic</h2>
                <h2>Designing an API for Description Logic</h2>
            </section>
            <section>
                <h1>Sources</h1>
                <img src="/9780521873611.jpg" alt="Cover of the book An Introduction to Description Logic" />
                <img src="/9780521876254.jpg" alt="Cover of the book The Description Logic Handbook" />

            </section>
            <section>
                <h1>Expectations</h1>
                <p>I'm still learning this.</p>
                <p>Parts of this talk were researched/written involuntarily by candle light</p>
                <p>I'm assuming you are interesting in DL, but maybe don't know much about it</p>
                <p>I'm not assuming you have a background in logic (I don't have one)</p>
                <p>Basic familiarity with programming (Python, JS, SQL, bash, regex, etc.)</p>
                <p>Basic familiarity with RDF</p>
                <p>Not focusing on the Linked Data side of DL, happy to discuss though</p>
                <p>Hopefully connections between DL and OWL clear.</p>
                <p>Minor renaming Concepts instead of Classes and Roles instead of Properties.</p>
            </section>
        </section>
        <section>
            <section>
                <h1>Background & History</h1>
            </section>
            <section>
                <h1>What is Description Logic?</h1>
                <p>A System of Logic Designed to aid in Terminological Knowledge Representation</p>
                <p>At One Point Called "Terminological Knowledge Representation Languages" or "Concept Languages"</p>
                <p>Concerned with fomally defining relationships between concepts and roles</p>
                <p>Still an active area of research <a href="https://dl.kr.org">dl.kr.org</a></p>
            </section>
            <section>
                <h1>What are Description Logics?</h1>
                <p>A family of languages</p>
                <p>Each provides a different level of expressiveness</p>
                <p>Names are made up of letters like <img alt="AL written in script" src="/al.svg"> and <img alt="SROIQ^(D) written in script" src="/sroiq(d).svg"></p>
                <p>The rules for naming are a little confusing 🤷‍♀️</p>
                <p>Differences between different languages can include different ways of supporting negation, unions, cardinal restriction, inversion, role heirarchies, etc</p>
                <p>The trade off in expressiveness is complexity of the reasoner and time/decidability</p>
            </section>
            <section>
                <h1>Why Use Logic?</h1>
                <p>First-Order Logic allows us to model with objects and predicates</p>
                <code>Likes(jv24601, bread)</code>
                <p>It also provides quantifiers and variables</p>
                <code>∀<i>x</i>French(<i>x</i>) → Likes(<i>x</i>, bread)</code>
                <p>And operators for combining expressions.</p>
                <code>French(jv24601) ⋀ Likes(jv24601, bread)</code>
            </section>
            <section>
                <h1>Description Logic's Relationship to First-Order Logic</h1>
                <p>DL can be thought of as a syntactic shorthand for a subset of FOL</p>
                <p>An example from pg 2 of An Introduction to Description Logic</p>
                <p>The following statements are equivalent between FOL and DL</p>
                <p>In FOL</p>
                <code>∀<i>x</i>(Teacher(<i>x</i>) ⇔ Person(<i>x</i>) ⋀ ∃<i>y</i> (<i>teaches</i>(<i>x</i>, <i>y</i>) ⋀ Course(<i>y</i>))) </code>
                <p>In DL</p>
                <code>Teacher ≡ Person ⊓ ∃teaches.Course</code>
            </section>
            <section>
                <h1>History</h1>
                <p>This is a little speculative, don't take it too seriously.</p>
                <p>Developed out of ideas like semantic networks from natural language processing</p>
                <p>Its big development was adding the separate logic language that let you describe additional relationships beyond what was directly stored in the network</p>
                <p>Loosely considered part of AI today, but was considered more relevant to AI research in the 80's and 90's</p>
                <p>Rigidness led to loss of interest in the AI field as ML became more popular</p>
                <p>Still useful where rigidness is a virtue (configuration, scheduling, vocabularies, other reasoning tasks)</p>
            </section>
        </section>
        <section>
            <section>
                <h1>Description Logic At a High Level</h1>
                <p>Knowledge Bases</p>
                <p>&nbsp;&nbsp;ABox</p>
                <p>&nbsp;&nbsp;TBox</p>
                <p>Operatations and Properties of KB, TBoxes, and ABoxes</p>
            </section>
            <section>
                <h1>Knowledge Base</h1>
                <p>A Structure made up of two parts a TBox and an ABox</p>
                <p>Most of DL is concerned with properties of knowledge bases</p>
            </section>
            <section>
                <h1>ABox</h1>
                <p>Made up of unary and binary predicates</p>
                <p>Unary predicates act like is-a style relationships</p>
                <code>betty: Cat</code>
                <p>Can include full expressions</p>
                <code>betty: Cat ⊓ ¬Dog ⊓ Animal</code>
                <p>Binary predicates are like triples</p>
                <code>(betty, 11/11/2021): dob</code>
            </section>
            <section>
                <h1>Concept</h1>
                <p>When we have something like</p>
                <code>x: A</code>
                <p>"The object x extends the concept A."</p>
            </section>
            <section>
                <h1>Role</h1>
                <p>Relateds two elements.</p>
                <code>(betty, 11/11/2021): dob</code>
            </section>
            <section>
                <h1>TBox</h1>
                <p>The TBox defines terms such as concept names or role names that are referenced in the ABox</p>
                <p>These are called concept descriptions and role descriptions.</p>
                <p>With description logics that allow for complex role relationships an RBox might also be</p>
                <code>Cat ⊑ Animal</code>
                <p>"All Cats are Animals."</p>
            </section>
            <section>
                <h1>An Example Knowledge Base</h1>
                <table class="reveal">
                    <tr><th>TBox</th></tr>
                    <tr><td><code>Cat ⊑ Animal</code></td></tr>
                    <tr><th>ABox</th></tr>
                    <tr><td><code>betty : Cat</code></td></tr>
                </table>
            </section>
            <section>
                <h1>Defining <img alt="AL written in script" src="/al.svg"></h1>
                <p>Syntax</p>
                <p>Atomic Concepts - <code>Cat Animal French</code></p>
                <p>Top and Bottom - <code>⊤ ⊥</code></p>
                <p>Atomic Negation - <code>¬Cat ¬Animal ¬French</code></p>
                <p>Intersection - <code>Cat ⊓ Fish</code></p>
                <p>Value Restriction - <code>∀R.C, ∀likes.⊤ ∀likes.Item</code></p>
                <p>Limited Existential Quantification - <code>∃R.⊤, ∃likes.⊤</code>, only <code>⊤</code> is supported</p>
            </section>
            <section>
                <h1>Terminological Axioms</h1>
                <p>Usually take the form</p>
                <p>Equalities</p>
                <code>A ≡ B</code>
                <p>Inclusions</p>
                <code>A ⊑ B</code>
            </section>
            <section>
                <h1>Example in <img alt="AL written in script" src="/al.svg"/></h1>
                <pre><code>
Feline ≡ Cat,
Cat ⊑ Mammal,
Canine ≡ Dog,
Dog ⊑ Mammal,
Mammal ⊑ Animal,
Cat ≡ ¬Dog,
Dog ≡ ¬Cat,
Animal ≡ ∃dob.⊤ ⊓ ∃name.⊤
                </code></pre>
            </section>
        </section>
        <section>
            <section>
                <h1>Interpreting Knowledge Bases</h1>
                <p>Creates a model from a knowledge base</p>
                <p>Usually expressed as a graph or a table that enumerates all values in a model</p>
            </section>
            <section>
                <h1>Using a Table</h1>
                <pre><code data-trim data-noescape>
Cat ⊑ Animal,
betty : Cat,
(betty, peggy): sibling
                </code></pre>
                <table class="reveal">
                    <tr><th>∆</th><td>betty, peggy</td></tr>
                    <tr><th>Cat</th><td>betty</td></tr>
                    <tr><th>Animal</th><td>betty</td></tr>
                    <tr><th>sibling</th><td>(betty, peggy)</td></tr>
                </table>
            </section>
            <section>
                <h1>Using a Graph</h1>
                <pre><code data-trim data-noescape>
Cat ⊑ Animal,
betty : Cat,
(betty, peggy): sibling
                </code></pre>
                <img alt="graph of a node labled betty Animal Cat that points to a node labled Peggy and the arrow is labeled sibling" src="/graphviz.png" />
            </section>
            <section>
                <h1>Consistency</h1>
                <p>Consistency is very important to DL</p>
                <p>A Knowledge Base is considered consistent if it does contain any clashes</p>
                <p>A clash is when an element is said to both be in the extension of a concept and not be in the extension of a concept</p>
                <p>A simple example</p>
                <pre><code>
betty: Cat, 
betty: ¬Cat
                </code></pre>
                <p>A slightly more complex example.</p>
                <pre><code>
Cat ⊑ Animal,
betty: Cat,
betty: ¬Animal</code></pre>
                <p>The above only has a clash after inferencing, if you removed the first statement it'd be fine.</p>
                <pre><code>
betty: Cat, 
betty: ¬Animal</code></pre>
            </section>
        </section>
        <section>
            <section>
                <h1>Manipulating Concept Languages</h1>
                <p>Normalization rules let us simplify expressions like</p>
                <code>Animal ≡ ¬(Cat ⊓ Dog)</code>
                <p>To</p>
                <code>Animal ≡ ¬Cat ⊔ ¬Dog</code>
                <p>We can also simplify ABoxes</p>
                <code>betty: Cat ⊓ ¬Dog</code>
                <p>To</p>
                <code>betty: Cat, betty: ¬Dog</code>
            </section>
            <section>
                <h1>Manipulating Concept Languages (2)</h1>
                <p>Some more examples</p>
                <code>Cat ≡ Animal ⊓ Liquid</code>
                <p>Becomes</p>
                <pre><code data-trim data-noescape>
Cat ⊑ Animal ⊓ Liquid
Animal ⊓ Liquid ⊑ Cat
                </code></pre>
                <p>Becomes</p>
                <pre><code data-trim data-noescape>
¬Cat ⊔ (Animal ⊓ Liquid)
¬(Animal ⊓ Liquid) ⊔ Cat
                </code></pre>
                <p>Becomes</p>
                <pre><code data-trim data-noescape>
¬Cat ⊔ (Animal ⊓ Liquid)
¬Animal ⊔ ¬Liquid ⊔ Cat
                </code></pre>
            </section>
            <section>
                <h1>Tableau Algorithm</h1>
                <p>Used to answer questions about knowledge bases</p>
                <p>Given</p>
                <pre><code data-trim data-noescape>
Cat ⊑ Animal,
betty : Cat
                </code></pre>
                <p>We can ask the question</p>
                <p>Is betty an Animal?</p>                
                <p>To check this we check the opposite, if betty isn't an animal, and if we find a contradiction then we know betty is an Animal.</p>
                <p>First we rewite the ⊑ as follows.</p>
                <pre><code data-trim data-noescape>
¬Cat ⊔ Animal,
betty : Cat,
betty : ¬Animal
                </code></pre>
                <p>Now we test what we know against this rule.</p>
                <p>The left hand side of the disjunction immedately clashes since we know Betty is a Cat.</p>
                <p>The right hand side also clashes since we are assuming betty isn't an Animal.</p>
                <p>So we know that Betty is an Animal.</p>
            </section>
        </section>
        <section>
            <section>
                <h1>Designing an API for Description Logic</h1>
            </section>
            <section>
                <h1>Why?</h1>
                <p>Explore using reasoning and ontologies for more problems</p>
                <p>Without requiring entire semantic web stack</p>
                <p>Without requiring a separate programming language</p>
                <p>Simple enough but potentially still useful</p>
                <p>"Semantic Calculator"</p>
            </section>
            <section>
                <h1>Simplicity</h1>
                <p>Just uses Strings for element names, concept names, role names, etc.</p>
                <p>Very few operations</p>
                <p>Express concept languages as data structures</p>
                <p>Use triples-like structure for storing data</p>
            </section>
            <section>
                <h1>Storing ABox Values</h1>
                <p>Store role information using techniques for triples (something as simple as a set of tuples to something more complete like hexastore)</p>
                <p>Store Concept extension information in key-value/multi-map like store</p>
                <p>Store both Concept extension and non-extension to aid with finding clashes</p>
                <p>Fake TypeScript</p>
                <pre><code data-trim data-noescape>
type ConceptName = string;
type RoleName = string;
type Element = string;
interface Extension = &lbrace; type: "extension", element: Element, concept: ConceptName &rbrace;
interface NonExtension = &lbrace; type: "non-extension", element: Element, concept: ConceptName &rbrace;
interface Role = &lbrace; type: "role", first: Element, second: Element, role: RoleName &rbrace;
type ABox = Set&lt;Extension | NonExtension | Role&gt;
                </code></pre>
            </section>
            <section>
                <h1>Representing Concept Languages</h1>
                <p>Use whatever modeling is supplied by the host language to best support complex structures</p>
                <p>ADTs in typed-functional languages</p>
                <p>Interface/Class heirarchies in typed-OOP languages</p>
                <p>YMMV in dynamic languages</p>
                <p>Fake TypeScript</p>
                <pre><code data-trim data-noescape>
interface ConceptInclusion = &lbrace; type: "inclusion", left: Concept, right: Concept &rbrace;
interface ConceptDefinition = &lbrace; type: "inclusion", left: ConceptName, right: Concept &rbrace;
...
type Concept = AtomicConcept | ConceptConjunction | ConceptDisjuntion | AtomicNegation;
                </code></pre>
            </section>
            <section>
                <h1>Operations</h1>
                <p><code>read</code> - read in DL expressions and create datastructures (not needed for simple use cases)</p>
                <p><code>interpret</code> - take in representations of a TBox and ABox and return a model</p>
                <p>Possibily also functions to check for completeness, consistency/clashes, etc.</p>
                <p>Fake Typescript</p>
                <pre><code data-trim data-noescape>
const res = read("Cat ⊑ Animal, betty: Cat")
&gt; res = [&lbrace; type: "inclusion", left: "Cat", right: "Animal" &rbrace;,
&lbrace; type: "etension", element: "betty", concept: "Cat" &rbrace;]
const model = interpret(res)
&gt; model = [&lbrace; type: "inclusion", left: "Cat", right: "Animal" &rbrace;,
&lbrace; type: "etension", element: "betty", concept: "Cat" &rbrace;,
&lbrace; type: "etension", element: "betty", concept: "Animal" &rbrace;]
                </code></pre>
            </section>
            <section>
                <h1>tiny-dl</h1>
                <p>Status: proof of concept</p>
                <p>F# / Rust implementations (mostly F# for now)</p>
                <p>Targets .NET Core & JS (eventually native and wasm via Rust)</p>
                <p>MPL 2.0 license</p>
                <p><a href="https://github.com/almibe/ligature-fs/tree/main/src/tiny-dl">https://github.com/almibe/ligature-fs/tree/main/src/tiny-dl</a></p>
            </section>
        </section>
    </div>
</div>

<style>
@font-face {
    font-family: 'Comfortaa';
    src: url('/font/Comfortaa-VariableFont_wght.ttf');
}

@font-face {
    font-family: 'Raleway';
    src: url('/font/Raleway-VariableFont_wght.ttf');
}

@font-face {
    font-family: 'SourceCodePro';
    src: url('/font/SourceCodePro-VariableFont_wght.ttf');
}

h1, h2, h3, h4, h5, h6 {
    font-family: 'Comfortaa';
}

p, div {
    font-family: 'Raleway';
}

h1 {
    font-size: xx-large;
}

h2 {
    font-size: x-large;
}

pre {
    text-align: start;
    width: 50%;
    float:none;
}

table, tr {
  border-collapse: collapse;
  border: 1px solid;
}

code {
    font-family: 'SourceCodePro';
}
</style>