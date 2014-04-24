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
>       <p>Последнее изменение: 2001-04-23</p>
>       <p>Автор: fred@example.com</p>
>     </section>
>
> Однако, это было бы лучше разметить как:
>
>     <section>
>       <footer>Последнее изменение: 2001-04-23</footer>
>       <address>Автор: fred@example.com</address>
>     </section>
>
> Или:
>
>     <section>
>       <footer>
>         <p>Последнее изменение: 2001-04-23</p>
>         <address>Автор: fred@example.com</address>
>       </footer>
>     </section>

Ладно, это не так впечатляет, но всё же, применение более подходящих тегов
`footer` и `address` — это круто. Считая, что я уже знаю всё, что можно знать
про семантику абзацев, я увидел такое примечание в спеках:

> Решение состоит в понимании того, что абзац, в понимании HTML, не логическое
> понятие, а структурное. В фантастическом примере [ниже], фактически пять
> абзацев, как определяется в этой спецификации: один перед списком, по одному
> на каждый элемент и один после списка.

    <p>К примеру, это фантастическое предложение содержит пункты про</p>
    <ul><li>колдунов,
      <li>перемещение быстрее скорости света и
      <li>телепатию,</ul>
    <p>и подробнее рассматривается ниже.</p>

Другими словами, «[нет никакой ложки][5]».

## Сквозная модель h1-h6

План документа (Document Outline), введённый в HTML5 и позволяющий
использовать несколько тегов `h1`—`h6`, основываясь на разделении документа на
разделы, [*не* существует][6].

> Это принцип, который живёт в спецификации HTML, но по сути является
> фикцией в реальном мире. Это фикция потому что в браузерах он не
> воплощен, и нет никакого намёка, что когда-нибудь будет. — [Стив Фолкнер][7] 

Честно говоря, для меня слышать такое — это своего рода облегчение, потому как
мне никогда не казалась удобной или понятной концепция множественных элементов
`h1` или `h2` на странице. Чувство неуклюжести быстро нарастало при попытках
вспомнить, какие из элементов начинают новый [контекст раздела][8], и сколько
заголовков я уже использовал. Простота — это здорово.

## Разметка документации

Я сейчас занимаюсь исследованиями в области документации для разработчиков,
и мне захотелось взглянуть на теги `pre` и `code`, чтобы убедиться, что я
правильно их использую. `code` для ссылок внутри предложения, как например
внутри этого, и `pre` для длинных кусков кода наподобие `blockquote`.

Что ж, эти допущения оказались в основном верными, но как я увидел, обычно
удаётся подобрать более подходящие и более выразительные элементы.
Я обнаружил ещё пару элементов, которые были специально созданы для
документации кода, [`kbd`][9] и [`samp`][10]. Для меня они особенно значимы,
потому что решают две задачи:

*   Теперь я при помощи семантики элемента могу разделять код, который
    пользователь должен ввести (`kbd`), и код, который машина ему выведет
    (`samp`).

*   Теперь я могу указывать различные стили в CSS, чтобы визуально различать
    в документации эти куски информации.

Я раньше никогда их не встречал в разметке документации, но теперь я просто
не могу представить, чтобы я их не использовал.

## Детализация кода

Если мы хотим быть действительно выразительными, то есть ещё парочка
элементов, которые мы можем использовать, чтобы сделать разметку более
читаемой как для людей, так и для машин.

Тег [`var`][11] можно использовать для разметки переменных в коде, а элемент
[`data`][12] для описания чистых данных, например, значений в табличном виде.

Вы можете поинтересоваться, какие же премущества дают элементы `data` перед
атрибутами `data-*`. `data` можно установить атрибут `value`, и
когда-нибудь браузеры научатся использовать его совместно с атрибутом
[`sortable`][13] элемента `table`, предоставляя авторам и пользователям
механизм [сортировки таблиц][14].

**Примечание:** Что касается поддержки браузерами сортировки таблиц, то тут
есть большие пробуксовки, и я пока не видел ни одного рабочего примера.
К тому же, раздел спецификации API DOM в HTML 5.1, посвященный этому,— 
это сплошная каша. Но когда это появится в браузерах, не забудьте указать
роли [`aria-sort`][15] нужным элементам заголовка таблицы. (Спасибо
[Рею Камдену][16] за ликбез.)

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