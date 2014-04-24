В 2014 году говоря о семантике в HTML мы вполне довольны результатами.

Есть `section`, `header`, `aside`, `footer`, `main` и даже `menu`!
У нас в распоряжении есть всё необходимое, верно? Тогда почему же мы
продолжаем делать вот так?

    <body class="article">
    <div class="content">

Всякий раз, когда лень или нехватка времени вынуждали меня писать такие вещи,
мне было стыдно. И вот я решил освежить свои представления о том, как
правильно использовать наши [старые добрые стандарты разметки][1].
С чего ещё начать, как не с хорошо известного [тега div][2]? И сразу же
я наткнулся на такое примечание в спецификации:

> Авторам настоятельно рекомендуется рассматривать элемент div как элемент
> на крайний случай, когда никакой другой элемент не подходит. Использование
> более подходящих элементов, чем элемент div, обеспечивает большую
> понятность для читателей и более лёгкую поддержку для авторов.

Начало было безусловно хорошим, и я решил дальше пролистать документацию,
в поисках чего-нибудь, что позволило бы мне утвердиться во мнении.
Помните элемент `hr`? Что ж, оказывается, что он нужен не просто для рисования
посреди экрана линии с резными, скошенными или выпуклыми краями. На самом
деле, он [очень семантичен][3].

> Элемент hr представляет собой тематический разрыв уровня абзаца, т.е.
> изменение места действия в истории, или переход к другой теме внутри
> раздела в справочнике.

Ух ты! Вот в этом месте мне мне стало действительно интересно. Я должен
узнать больше! Какими ещё допущениями я руководстовался когда верстал?

Как насчёт скромного [элемента абзаца][4]?

> Элемент p не следует применять, когда есть более подходящие
> узкоспециализированные элементы. Следующий пример технически корректен:
>
>     <section>
>       <p>Last modified: 2001-04-23</p>
>       <p>Author: fred@example.com</p>
>     </section>
>
> Однако, это было бы лучше разметить как:
>
>     <section>
>       <footer>Last modified: 2001-04-23</footer>
>       <address>Author: fred@example.com</address>
>     </section>
>
> Или:
>
>     <section>
>       <footer>
>         <p>Last modified: 2001-04-23</p>
>         <address>Author: fred@example.com</address>
>       </footer>
>     </section>

Ладно, это не так впечатляет, но всё же, применение более подходящих тегов
`footer` и `address` — это круто. Считая, что я уже знаю всё, что можно знать
про семантику абзацев, я увидел такое примечание в спеках:

> Решение состоит в понимании того, что абзац, в понимании HTML, не логическое
> понятие, а структурное. В фантастическом примере [ниже], фактически пять
> абзацев, как определяется в этой спецификации: один перед списком, по одному
> на каждый элемент и один после списка.

    <p>For instance, this fantastic sentence has bullets relating to</p>
    <ul><li>wizards,
      <li>faster-than-light travel, and
      <li>telepathy,</ul>
    <p>and is further discussed below.</p>

Другими словами, «[нет никакой ложки][5]».

## The single h1-h6 model

The HTML5 Document Outline, that allows for multiple `h1-h6` tags based on
sectioning roots,[does *not* exist][6].

> Is a concept that lives in the HTML specification, but is essentially a
> fiction in the real world. It is a fiction because user agents have not
> implemented it and there is no indication that any will. - [Steve Faulkner][7]

To be honest, it’s kind of a relief to hear this, because I never felt
comfortable or totally grasped the concept of multiple`h1` or `h2` elements on
a page. It quickly became unweildy when trying to remember which elements began
a new [section context][8], and how many header elements I’d already used.
Cheers for keeping things simple.

## Marking up documentation

As I’m currently doing research on developer documentation, I thought I’d
look into`pre` and `code` tags, to be sure I was using them correctly. `code`
for inline references, like in this paragraph, and`pre` for longer,
`blockquote`-style code embeds.

Well, those assumptions are mostly true, but as we’ve seen, there is usually
a better, more meaningful element to use. What I found was another pair of
elements that were specifically created for code documentation,[`kbd`][9] and
[`samp`][10]. Why these tags are so special to me is that they solve 2 problems:

*   I can now use a semantic element to distinguish between code that the user
    should enter
    (`kbd`) and code that a machine outputs (`samp`).

*   I now have 2 separate CSS hooks to use to help visually distinguish these
    two pieces of information in documentation.

I’d never seen those applied to documentation markup before, but now I can’t
imagine not using them.

## Code granularity

If we want to get really descriptive, there are a couple more elements we can
leverage for both machine and human-readable code markup.

The [`var`][11] tag can be used for marking up variables in code, and the
[`data`][12] element is used to delineate pure data, such as the values needed
in tabular information.

You might be asking what the `data` element offers over `data-*` attributes.
With the`data` element’s `value` attribute present, browsers will someday be
able to use it with the[`sortable`][13] attribute of the `table` element to
provide a mechanism for authors and users to[sort tables][14].

*Note:* Browser support for the table sorting model very hard to come by, and
I've yet to see a working example. Plus, the HTML 5.1 DOM API spec on it is kind
of a mess, but when it does make it into in the wild, make sure you add the
[`aria-sort`][15] role to the appropriate table header element. (Thanks to
[Ray Camden][16] for shedding some light.)

Another highly useful element in code documentation semantics is the `figure`
element, and it can be used for much more than screenshots.

> The figure element represents some flow content, optionally with a caption,
> that is self-contained (like a complete sentence) and is typically referenced as
> a single unit from the main flow of the document.


Notice nothing about images specifically was mentioned. The spec then goes on
to demo a code snippet marked up with `figure`.

    <p>In <a href="#l4">listing</a> we see the primary core interface
    > API declaration.</p>
    <figure id="l4">
      <figcaption>Listing 4. The primary core interface API declaration.</figcaption>
      
      interface PrimaryCore {
        boolean verifyDataLine();
        void sendData(in sequence<byte> data);
        void initSelfDestruct();
      }
      
    </figure>
    <p>The API is designed to use UTF-8.</p>


Wow, that totally makes sense, doesn’t it? Think about how many books you’
ve read that have[this little figure element][17] off to the side to point out
a detail about a code snippet.

## Description Lists: the unsung workhorses

My favorite HTML element, and in my opinion, the most underrated element in the
spec, is the decription list
([`dl`][18]). It’s intended for marking up name-value pairs of content. This
could apply to anything from a list of services offered and their accompanying
descriptions, to a simple ‘previous article/next article’ component, like the
one at the bottom of every article on my blog here. It’s perfect for documenting
a page’s edit history, causes and effects, or, surprisingly, any list data that
needs a group heading. I had no idea before reading the spec, but it’s entirely
valid to have one`dt` (decription term) and multiple `dd`s (description
definitions). Here’s a great example from the spec, marking up variations in
spelling across the English language, though the definition is the same.

    <dl>
      <dt lang="en-US"> <dfn>color</dfn> </dt>
      <dt lang="en-GB"> <dfn>colour</dfn> </dt>
      <dd> A sensation which (in humans) derives from the ability of
      the fine structure of the eye to distinguish three differently
      filtered analyses of a view. </dd>
    </dl>

Astute readers and fellow HTML nerds may be wondering about the rarely-seen
[`dfn`][19] element and where it fits into the semantic uses of description
lists. A`dfn` is the element the spec describes as: “the defining instance of
a term”. In combination with the`abbr` and `a` elements, one can provide a
really nice UX for finding the first instance of a definiton. See this example
from the spec:

> In the following fragment, the term “Garage Door Opener” is first defined
> in the first paragraph, then used in the second. In both cases, its abbreviation
> is what is actually displayed.

    <p>The <dfn><abbr title="Garage Door Opener">GDO</abbr></dfn>
    is a device that allows off-world teams to open the iris.</p>
    <!-- ... later in the document: -->
    <p>Teal'c activated his <abbr title="Garage Door Opener">GDO</abbr>
    and so Hammond ordered the iris to be opened.</p>
    With the addition of an a element, the reference can be made explicit:
    
    <p>The <dfn id=gdo><abbr title="Garage Door Opener">GDO</abbr></dfn>
    is a device that allows off-world teams to open the iris.</p>
    <!-- ... later in the document: -->
    <p>Teal'c activated his <a href=#gdo><abbr title="Garage Door Opener">GDO</abbr></a>
    and so Hammond ordered the iris to be opened.</p>


If you’ve ever read an ebook that has footnote or index functionality, this
is exactly the same idea.

## Just the beginning

While there is still [work to be done][20] on the available semantics and
appropriate uses of markup, it’s nice to know that we have more to work with
than we sometimes allow ourselves to believe.

In my next post, we’ll dive deeper into the HTML of tomorrow, and what it
would look like if it were designed today.

 [1]: https://developer.mozilla.org/en-US/docs/Web/HTML
 [2]: http://www.w3.org/html/wg/drafts/html/master/grouping-content.html#the-div-element
 [3]: http://www.w3.org/html/wg/drafts/html/master/grouping-content.html#the-hr-element
 [4]: http://www.w3.org/html/wg/drafts/html/master/grouping-content.html#the-p-element
 [5]: http://www.youtube.com/watch?v=XO0pcWxcROI
 [6]: http://blog.paciellogroup.com/2013/10/html5-document-outline/
 [7]: http://kevinsuttle.com/posts/the-art-of-html-semantics-pt1/twitter.com/stevefaulkner
 [8]: http://www.w3.org/TR/html5/sections.html#outlines
 [9]: http://www.w3.org/html/wg/drafts/html/master/text-level-semantics.html#the-kbd-element

 [10]: http://www.w3.org/html/wg/drafts/html/master/text-level-semantics.html#the-samp-element
 [11]: http://www.w3.org/html/wg/drafts/html/master/text-level-semantics.html#the-var-element
 [12]: http://www.w3.org/html/wg/drafts/html/master/text-level-semantics.html#the-data-element
 [13]: http://www.w3.org/html/wg/drafts/html/master/tabular-data.html#attr-table-sortable
 [14]: http://www.w3.org/html/wg/drafts/html/master/tabular-data.html#table-sorting-model
 [15]: http://www.w3.org/TR/wai-aria/states_and_properties#aria-sort
 [16]: http://www.raymondcamden.com/
 [17]: http://www.codinghorror.com/blog/2007/12/on-the-meaning-of-coding-horror.html
 [18]: http://www.w3.org/TR/html5/grouping-content.html#the-dl-element
 [19]: http://www.w3.org/TR/html5/text-level-semantics.html#the-dfn-element

 [20]: http://alistapart.com/comments/battle-for-the-body-field#336421