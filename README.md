# Airbnb Przewodnik po stylu JavaScript() {

*Najbardziej rozsądne podejście do JavaScript*

> **Uwaga**: ten przewodnik zakłada, że używasz [Babel](https://babeljs.io), i wymaga użycia [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) lub odpowiednika. Zakłada również, że instalujesz shims/polyfills w swojej aplikacji za pomocą [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims) lub odpowiednika.

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Ten przewodnik jest dostępny również w innych językach. Zobacz [tłumaczenie](#tłumaczenie)

Inne przewodniki po stylach

  - [ES5 (Przestarzały)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
  - [React](react/)
  - [CSS-in-JavaScript](css-in-javascript/)
  - [CSS & Sass](https://github.com/airbnb/css)
  - [Ruby](https://github.com/airbnb/ruby)

## Spis treści

  1. [Typy](#typy)
  1. [Referencje](#referencje)
  1. [Obiekty](#obiekty)
  1. [Tablice](#tablice)
  1. [Destrukturyzacja](#destrukturyzacja)
  1. [Stringi](#stringi)
  1. [Funkcje](#funkcje)
  1. [Funkcje strzałkowe](#funkcje-strzałkowe)
  1. [Klasy & konstruktory](#klasy--konstruktory)
  1. [Moduły](#moduły)
  1. [Iteratory i generatory](#iteratory-i-generatory)
  1. [Właściwości](#właściwości)
  1. [Zmienne](#zmienne)
  1. [Hoisting](#hoisting)
  1. [Operatory porównania i równości](#operatory-porównania-i-równości)
  1. [Blocks](#blocks)
  1. [Control Statements](#control-statements)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Type Casting & Coercion](#type-casting--coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [Events](#events)
  1. [jQuery](#jquery)
  1. [ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  1. [ECMAScript 6+ (ES 2015+) Styles](#ecmascript-6-es-2015-styles)
  1. [Standard Library](#standard-library)
  1. [Testowanie](#testowanie)
  1. [Wydajność](#wydajność)
  1. [Resources](#resources)
  1. [In the Wild](#in-the-wild)
  1. [Tłumaczenie](#tłumaczenie)
  1. [The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Współtwórcy](#współtwórcy)
  1. [Licencja](#licencja)
  1. [Poprawki](#poprawki)

## Typy

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **Prymitywne**: Kiedy uzyskujesz dostęp do typu prymitywnego, pracujesz bezpośrednio na jego wartości.

    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`
    - `bigint`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

    - Symbole i BigInts nie mogą być wiernie wypełniane, więc nie należy ich używać podczas targetowania przeglądarek / środowisk, które nie obsługują ich natywnie.

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **Złożone**: Kiedy uzyskujesz dostęp do typu złożonego, pracujesz na referencji do jego wartości.

    - `object`
    - `array`
    - `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ powrót do góry](#spis-treści)**

## Referencje

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) Użyj `const` dla wszystkich twoich referencji; unikaj używania `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > Czemu? To gwarantuje, że nie będziesz mógł ponownie przypisać swoich referencji, co może prowadzić do błędów i trudnego do zrozumienia kodu.

    ```javascript
    // złe
    var a = 1;
    var b = 2;

    // dobre
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) Jeśli musisz zmienić przypisanie referencji, użyj `let` zamiast `var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > Czemu? `let` ma raczej zasięg blokowy niż funkcjonalny `var`.

    ```javascript
    // złe
    var count = 1;
    if (true) {
      count += 1;
    }

    // dobre, użyj let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) Zauważ, że oba `let` i `const` mają zasięg blokowy.

    ```javascript
    // const i let istnieją tylko w blokach, w których są zdefiniowane.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ powrót do góry](#spis-treści)**

## Obiekty

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) Użyj literalnej składni do tworzenia obiektów. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // złe
    const item = new Object();

    // dobre
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) Używaj obliczonych nazw właściwości podczas tworzenia obiektów z dynamicznymi nazwami właściwości.

    > Czemu? Pozwalają zdefiniować wszystkie właściwości obiektu w jednym miejscu.

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // złe
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // dobre
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) Użyj metody obiektowej shorthand. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    ```javascript
    // złe
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // dobre
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) Użyj wartości właściwości shorthand. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > Czemu? Jest krótszy i opisowy.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // złe
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // dobre
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) Zgrupuj właściwości shorthand na początku deklaracji obiektu.

    > Czemu? Łatwiej jest powiedzieć, które właściwości używają shorthand.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // złe
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // dobre
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) Podaj tylko właściwości, które są niepoprawnymi identyfikatorami. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

    > Czemu? Ogólnie uważamy, że jest subiektywnie łatwiejszy do odczytania. Poprawia podświetlanie składni, a także jest łatwiej zoptymalizowany przez wiele silników JS.

    ```javascript
    // złe
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // dobre
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) Nie wywołuj metod `Object.prototype` bezpośrednio, tak jak `hasOwnProperty`, `propertyIsEnumerable`, i `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > Czemu? Metody te mogą być zaciemnione przez właściwości danego obiektu - rozważ `{ hasOwnProperty: false }` - lub, obiekt może być obiektem null (`Object.create(null)`).

    ```javascript
    // złe
    console.log(object.hasOwnProperty(key));

    // dobre
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // best
    const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
    console.log(has.call(object, key));
    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    console.log(has(object, key));
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) Preferuj object spread operator nad [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) do obiektów shallow-copy. Użyj object rest operator, aby uzyskać nowy obiekt z pominięciem niektórych właściwości.

    ```javascript
    // bardzo złe
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
    delete copy.a; // so does this

    // złe
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // dobre
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Tablice

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals)Użyj literalnej składni do tworzenia tablicy. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // złe
    const items = new Array();

    // dobre
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) Użyj [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) zamiast bezpośredniego przypisania, aby dodać elementy do tablicy.

    ```javascript
    const someStack = [];

    // złe
    someStack[someStack.length] = 'abracadabra';

    // dobre
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) Użyj array spreads `...` aby kopiować tablice.

    ```javascript
    // złe
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // dobre
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) Aby przekonwertować obiekt iterable object na tablicę, użyj spreads `...` zamiast [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // dobre
    const nodes = Array.from(foo);

    // najlepsze
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) Użyj [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) do konwersji obiektu podobnego do tablicy na tablicę.

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // złe
    const arr = Array.prototype.slice.call(arrLike);

    // dobre
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) Użyj [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) zamiast spread `...` do mapowania przez iterable, ponieważ unika się tworzenia tablicy pośredniej.

    ```javascript
    // złe
    const baz = [...foo].map(bar);

    // dobre
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) Używaj instrukcji return w wywołaniach zwrotnych metody tablicowej. Można pominąć return, jeśli treść funkcji składa się z pojedynczej instrukcji zwracającej wyrażenie bez skutków ubocznych, następująco [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // dobre
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // dobre
    [1, 2, 3].map((x) => x + 1);

    // źle - brak zwracanej wartości oznacza, że `acc` staje się niezdefiniowany po pierwszej iteracji
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
    });

    // dobre
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      return flatten;
    });

    // złe
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // dobre
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) Użyj podziałów linii po otwarciu i przed zamknięciem nawiasów tablicy, jeśli tablica ma wiele linii

    ```javascript
    // złe
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // dobre
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

**[⬆ powrót do góry](#spis-treści)**

## Destrukturyzacja

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) Użyj destrukturyzacji obiektów podczas uzyskiwania dostępu do wielu właściwości obiektu i korzystania z nich. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Czemu? Destrukturyzacja pozwala uniknąć tworzenia tymczasowych odniesień do tych właściwości.

    ```javascript
    // złe
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // dobre
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // najlepsze
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) Użyj destrukturyzacji tablic. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // złe
    const first = arr[0];
    const second = arr[1];

    // dobre
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) Użyj niszczenia obiektów dla wielu zwracanych wartości, a nie niszczenia tablic.

    > Czemu? Z czasem możesz dodawać nowe właściwości lub zmieniać kolejność rzeczy bez przerywania wywołań stron.

    ```javascript
    // złe
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // wywołujący musi pomyśleć o kolejności danych zwrotnych
    const [left, __, top] = processInput(input);

    // dobre
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // wywołujący wybiera tylko te dane, których potrzebuje
    const { left, top } = processInput(input);
    ```

**[⬆ powrót do góry](#spis-treści)**

## Stringi

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) Używaj pojedynczych cudzysłowów `''` dla stringów. eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

    ```javascript
    // złe
    const name = "Capt. Janeway";

    // źle - literały szablonów powinny zawierać interpolację lub znaki nowej linii
    const name = `Capt. Janeway`;

    // dobre
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) Stringi które powodują, że linia przekracza 100 znaków, nie należy pisać w wielu wierszach za pomocą konkatenacji łańcuchów.

    > Czemu? Przerwane stringi są ciężkie w pracy i sprawiają, że kod jest mniej przeszukiwalny.

    ```javascript
    // złe
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // złe
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // dobre
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) Podczas programowego budowania stringów należy używać ciągów szablonów zamiast konkatenacji. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > Czemu? Ciągi szablonów zapewniają czytelną, zwięzłą składnię z odpowiednimi znakami nowej linii i funkcjami interpolacji ciągów.

    ```javascript
    // złe
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // złe
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // złe
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // dobre
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) Nigdy nie używaj `eval()` na stringa, otwiera zbyt wiele luk w zabezpieczeniach. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) Do not unnecessarily escape characters in strings. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > Czemu? Ukośniki odwrotne szkodzą czytelności, dlatego powinny być obecne tylko wtedy, gdy jest to konieczne.

    ```javascript
    // złe
    const foo = '\'this\' \i\s \"quoted\"';

    // dobre
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ powrót do góry](#spis-treści)**

## Funkcje

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) Użyj nazwanych wyrażeń funkcyjnych zamiast deklaracji funkcji. eslint: [`func-style`](https://eslint.org/docs/rules/func-style)

    > Czemu? Deklaracje funkcji są hoisted, co oznacza, że łatwo - zbyt łatwo - odwołać się do funkcji, zanim zostanie zdefiniowana w pliku. Utrudnia to czytelność i łatwość konserwacji. Jeśli okaże się, że definicja funkcji jest na tyle duża lub wystarczająco złożona, że zakłóca zrozumienie reszty pliku, być może nadszedł czas, aby wyodrębnić ją do własnego modułu! Nie zapomnij wyraźnie nazwać wyrażenia, niezależnie od tego, czy nazwa jest wywnioskowana ze zmiennej zawierającej (co często ma miejsce w nowoczesnych przeglądarkach lub podczas korzystania z kompilatorów takich jak Babel). Eliminuje to wszelkie założenia dotyczące stosu wywołań błędu. ([Discussion](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // złe
    function foo() {
      // ...
    }

    // złe
    const foo = function () {
      // ...
    };

    // dobre
    // nazwa leksykalna odróżniona od wywołania (odwołań)
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) Zawiń natychmiast wywołane wyrażenia funkcyjne w nawiasach. eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife.html)

    > Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

    ```javascript
    // natychmiast wywoływane wyrażenie funkcyjne (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) Nigdy nie deklaruj funkcji w bloku niefunkcyjnym (`if`, `while`, etc). Zamiast tego przypisz funkcję do zmiennej. Przeglądarki pozwolą ci to zrobić, ale wszystkie interpretują to inaczej, co jest złą wiadomością. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **Uwaga:** ECMA-262 definiuje `block` jako listę instrukcji. Deklaracja funkcji nie jest instrukcją.

    ```javascript
    // złe
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // dobre
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
    - [7.5](#functions--arguments-shadow) Nigdy nie nazywaj parametru `arguments`. Będzie to miało pierwszeństwo przed obiektem `arguments`, który jest nadawany każdemu zakresowi funkcji.

    ```javascript
    // złe
    function foo(name, options, arguments) {
      // ...
    }

    // dobre
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) Nigdy nie używaj `arguments`, zdecyduj się zamiast tego na użycie składni rest syntax `...`. eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > Czemu? `...` wyraźnie określa, które argumenty chcesz wyciągnąć. Dodatkowo, argumenty rest są prawdziwym Array, a nie tylko podobne do Array jak `arguments`.

    ```javascript
    // złe
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // dobre
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) Użyj domyślnej składni parametrów zamiast mutować argumenty funkcji.

    ```javascript
    // naprawdę źle
    function handleThings(opts) {
      // No! We shouldn’t mutate function arguments.
      // Double bad: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // dalej źle
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // dobrze
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) Unikaj efektów ubocznych przy domyślnych parametrach.

    > Czemu? Są mylące.

    ```javascript
    var b = 1;
    // złe
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) Zawsze umieszczaj parametry domyślne na końcu.

    ```javascript
    // złe
    function handleThings(opts = {}, name) {
      // ...
    }

    // dobre
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) Nigdy nie używaj konstruktora funkcji do tworzenia nowej funkcji. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > Czemu? Utworzenie funkcji w ten sposób ocenia ciąg podobny do `eval()`, który otwiera luki w zabezpieczeniach.

    ```javascript
    // złe
    var add = new Function('a', 'b', 'return a + b');

    // dalej złe
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) Odstępy w podpisie funkcji. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > Czemu? Spójność jest dobra i nie trzeba dodawać ani usuwać spacji podczas dodawania lub usuwania nazwy.

    ```javascript
    // złe
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // dobre
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) Nigdy nie mutuj parametrów. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Czemu? Manipulowanie obiektami przekazywanymi jako parametry może powodować niepożądane zmienne skutki uboczne w pierwotnym obiekcie wywołującym.

    ```javascript
    // złe
    function f1(obj) {
      obj.key = 1;
    }

    // dobre
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) Nigdy nie przypisuj ponownie parametrów. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Czemu? Ponowne przypisanie parametrów może prowadzić do nieoczekiwanego zachowania, szczególnie podczas uzyskiwania dostępu do obiektu `arguments`. Może to również powodować problemy z optymalizacją, szczególnie w wersji V8.

    ```javascript
    // złe
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // dobre
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Preferuj uzycie operatora spread operator `...` aby wywoływać funkcje variadic. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > Czemu? Jest czyściej, nie musisz podawać kontekstu i nie możesz łatwo składać `new` z `apply`.

    ```javascript
    // złe
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // dobre
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // dobre
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // dobre
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) Funkcje z podpisami wielowierszowymi lub wywołaniami powinny być wcięte, tak jak każda inna lista wielowierszowa w tym przewodniku: każdy element w linii sam, z końcowym przecinkiem na ostatnim elemencie. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // złe
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // dobre
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // złe
    console.log(foo,
      bar,
      baz);

    // dobre
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ powrót do góry](#spis-treści)**

## Funkcje strzałkowe

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) Gdy musisz użyć funkcji anonimowej (tak jak przy przekazywaniu inline callback), użyj notacji funkcji strzałek. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

    > Czemu? Tworzy wersję funkcji, która działa w kontekście `this`, która jest zwykle tym, czego chcesz, i jest bardziej zwięzłą składnią.

    > Dlaczego nie? Jeśli masz dość skomplikowaną funkcję, możesz przenieść tę logikę do własnego nazwanego wyrażenia funkcji.

    ```javascript
    // złe
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // dobre
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) Jeśli ciało funkcji składa się z pojedynczej instrukcji zwracającej [wyrażenie](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)bez skutków ubocznych, pomiń nawiasy klamrowe i użyj domyślnego return. W przeciwnym razie zachowaj nawiasy klamrowe i użyj instrukcji `return`. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html)

    > Czemu? Czystość kodu. Czyta się dobrze, gdy połączonych jest wiele funkcji.

    ```javascript
    // złe
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // dobre
    [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

    // dobre
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // dobre
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // No implicit return with side effects
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // Do something if callback returns true
      }
    }

    let bool = false;

    // złe
    foo(() => bool = true);

    // dobre
    foo(() => {
      bool = true;
    });
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) W przypadku gdy wyrażenie obejmuje wiele wierszy, zawiń je w nawiasach, aby uzyskać lepszą czytelność.

    > Czemu? Pokazuje wyraźnie, gdzie funkcja zaczyna się i kończy.

    ```javascript
    // złe
    ['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // dobre
    ['get', 'post', 'put'].map((httpMethod) => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) Zawsze dołączaj nawiasy wokół argumentów dla jasności i spójności. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html)

    > Czemu? Minimalizuje rezygnację z różnic podczas dodawania lub usuwania argumentów.

    ```javascript
    // złe
    [1, 2, 3].map(x => x * x);

    // dobre
    [1, 2, 3].map((x) => x * x);

    // złe
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // dobre
    [1, 2, 3].map((number) => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // złe
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // dobre
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) Unikaj mylącej składni funkcji strzałek (`=>`) z operatorami porównania (`<=`, `>=`). eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // złe
    const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

    // złe
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // dobre
    const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

    // dobre
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) Wymuszaj lokalizację obiektów funkcji strzałek za pomocą niejawnych zwrotów. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // złe
    (foo) =>
      bar;

    (foo) =>
      (bar);

    // dobre
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
       bar
    )
    ```

**[⬆ powrót do góry](#spis-treści)**

## Klasy i konstruktory

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) Zawsze używaj `class`. Unikaj bezpośredniego manipulowania `prototype`.

    > Czemu? Składnia `class` jest bardziej zwięzła i łatwiejsza do uzasadnienia.

    ```javascript
    // złe
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // dobre
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) Użyj `extends` do dziedziczenia.

    > Czemu? Jest to wbudowany sposób na dziedziczenie prototypowej funkcjonalności bez przerywania `instanceof`.

    ```javascript
    // złe
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // dobre
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) Metody mogą zwracać wartość `this`, aby pomóc w tworzeniu łańcuchów metod.

    ```javascript
    // złe
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // dobre
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) Można napisać niestandardową metodę `toString()`, upewnij się tylko, że działa ona skutecznie i nie powoduje żadnych skutków ubocznych.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) Klasy mają domyślny konstruktor, jeśli nie został określony. Pusta funkcja konstruktora lub taka, która po prostu deleguje do klasy nadrzędnej, nie jest potrzebna. eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // złe
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // złe
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // dobre
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) Unikaj zduplikowanych członków klasy. eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > Czemu? Zduplikowane deklaracje członków klasy po cichu wolą ostatnią - posiadanie duplikatów jest prawie na pewno błędem.

    ```javascript
    // złe
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // dobre
    class Foo {
      bar() { return 1; }
    }

    // dobre
    class Foo {
      bar() { return 2; }
    }
    ```

  <a name="classes--methods-use-this"></a>
  - [9.7](#classes--methods-use-this) Metody klas powinny używać `this` lub zostać przekształcone w metodę statyczną, chyba że zewnętrzna biblioteka lub środowisko wymaga użycia określonych metod niestatycznych. Jako metoda instancji powinna wskazywać, że zachowuje się inaczej w zależności od właściwości receivera. eslint: [`class-methods-use-this`](https://eslint.org/docs/rules/class-methods-use-this)

    ```javascript
    // złe
    class Foo {
      bar() {
        console.log('bar');
      }
    }

    // dobrze - jest używane
    class Foo {
      bar() {
        console.log(this.bar);
      }
    }

    // dobrze - konstruktor jest zwolniony
    class Foo {
      constructor() {
        // ...
      }
    }

    // dobrze - metody statyczne nie powinny z tego korzystać
    class Foo {
      static bar() {
        console.log('bar');
      }
    }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Moduły

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) Zawsze używaj modułów (`import`/`export`) przez niestandardowy system modułowy. Zawsze możesz dokonać transpilacji do preferowanego systemu modułów.

    > Czemu? Moduły są przyszłością, zacznijmy korzystać z przyszłości już teraz.

    ```javascript
    // złe
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // najlepsze
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) Nie używaj wildcard imports.

    > Czemu? Dzięki temu masz tylko jeden domyślny eksport.

    ```javascript
    // złe
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // dobre
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) I nie eksportuj bezpośrednio z importu.

    > Czemu? Chociaż one-liner jest zwięzły, posiadanie jednego jasnego sposobu importowania i jednego jasnego sposobu eksportowania zapewnia spójność.

    ```javascript
    // złe
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // dobre
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) Importuj tylko ze ścieżki w jednym miejscu.
 eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)
    > Czemu? Posiadanie wielu wierszy importowanych z tej samej ścieżki może utrudnić utrzymanie kodu.

    ```javascript
    // złe
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // dobre
    import foo, { named1, named2 } from 'foo';

    // dobre
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) Do not export mutable bindings.
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    > Czemu? Ogólnie należy unikać mutacji, ale w szczególności podczas eksportowania mutable bindings. Chociaż ta technika może być potrzebna w niektórych szczególnych przypadkach, na ogół należy eksportować tylko constant references.

    ```javascript
    // złe
    let foo = 3;
    export { foo };

    // dobre
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) W modułach z pojedynczym eksportem preferuj domyślny eksport niż eksport nazwany.
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    > Czemu? Aby 'zachęcić' więcej plików, które kiedykolwiek eksportują tylko jedną rzecz. Jest to lepsze dla czytelności i konserwacji.

    ```javascript
    // złe
    export function foo() {}

    // dobre
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) Put all `import`s above non-import statements.
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
    > Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

    ```javascript
    // złe
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // dobre
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) Multiline imports should be indented just like multiline array and object literals.
 eslint: [`object-curly-newline`](https://eslint.org/docs/rules/object-curly-newline)

    > Czemu? Nawiasy klamrowe są zgodne z tymi samymi zasadami wcięcia, co każdy inny blok nawiasów klamrowych w przewodniku stylu, podobnie jak końcowe przecinki.

    ```javascript
    // złe
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // dobre
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) Nie zezwalaj na składnię modułu ładującego Webpack w instrukcjach importu modułu.
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)
    > Czemu? Ponieważ podczas importowania używa się składni Webpack, kod łączy się z pakietem modułów. Preferuj użycie składni modułu ładującego w `webpack.config.js`.

    ```javascript
    // złe
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // dobre
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

  <a name="modules--import-extensions"></a>
  - [10.10](#modules--import-extensions) Nie dołączaj rozszerzeń nazw JavaScript
 eslint: [`import/extensions`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/extensions.md)
    > Czemu? Dołączanie rozszerzeń hamuje refaktoryzację i niewłaściwe kodowanie szczegółów implementacji modułu importowanego do każdego konsumenta.

    ```javascript
    // złe
    import foo from './foo.js';
    import bar from './bar.jsx';
    import baz from './baz/index.jsx';

    // dobre
    import foo from './foo';
    import bar from './bar';
    import baz from './baz';
    ```

**[⬆ powrót do góry](#spis-treści)**

## Iteratory i generatory

  <a name="iterators--nope"></a><a name="11.1"></a>
  - [11.1](#iterators--nope) Nie używaj iteratorów. Wybieraj funkcje wyższego rzędu JavaScript zamiast takich jak pętle `for-in` lub `for-of`. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > Czemu? To wymusza naszą niezmienną zasadę. Radzenie sobie z czystymi funkcjami zwracającymi wartości jest łatwiejsze do uzasadnienia niż skutki uboczne.

    > Użyj `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... do iterowania po tablicach, i `Object.keys()` / `Object.values()` / `Object.entries()` do tworzenia tablic, dzięki czemu można iterować po obiektach.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // złe
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // dobre
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // najlepiej (użyj functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // złe
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // dobre
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // najlepiej (utrzymanie funkcjonalności)
    const increasedByOne = numbers.map((num) => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) Na razie nie używaj generatorów.

    > Czemu? Nie przenoszą się dobrze na ES5.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) Jeśli musisz użyć generatorów lub zignorujesz [naszą radę](#generators--nope), upewnij się, że podpis funkcji jest odpowiednio rozmieszczony. eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)

    > Czemu? `function` oraz `*` są częścią tego samego koncepcyjnego słowa kluczowego - `*` nie jest modyfikatorem dla `function`, `function*` jest unikalnym construct, innym niż `function`.

    ```javascript
    // złe
    function * foo() {
      // ...
    }

    // złe
    const bar = function * () {
      // ...
    };

    // złe
    const baz = function *() {
      // ...
    };

    // złe
    const quux = function*() {
      // ...
    };

    // złe
    function*foo() {
      // ...
    }

    // złe
    function *foo() {
      // ...
    }

    // bardzo złe
    function
    *
    foo() {
      // ...
    }

    // bardzo złe
    const wat = function
    *
    () {
      // ...
    };

    // dobre
    function* foo() {
      // ...
    }

    // dobre
    const foo = function* () {
      // ...
    };
    ```

**[⬆ powrót do góry](#spis-treści)**

## Właściwości

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) Używaj notacji kropkowej podczas uzyskiwania dostępu do właściwości. eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // złe
    const isJedi = luke['jedi'];

    // dobre
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) Użyj notacji nawiasowej `[]` podczas uzyskiwania dostępu do właściwości za pomocą zmiennej.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

  <a name="es2016-properties--exponentiation-operator"></a>
  - [12.3](#es2016-properties--exponentiation-operator) Użyj operatora potęgowania `**` przy obliczaniu wykładników. eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).

    ```javascript
    // złe
    const binary = Math.pow(2, 10);

    // dobre
    const binary = 2 ** 10;
    ```

**[⬆ powrót do góry](#spis-treści)**

## Zmienne

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) Zawsze używaj `const` lub `let` aby deklarować zmienne. Nieprzestrzeganie tego spowoduje globalne zmienne. Chcemy uniknąć zanieczyszczenia globalnej przestrzeni nazw. Kapitan Planeta nas przed tym ostrzegł. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // złe
    superPower = new SuperPower();

    // dobre
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) Użyj jednej deklaracji `const` lub `let` na zmienną lub przypisanie. eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html)

    > Czemu? W ten sposób łatwiej jest dodawać nowe deklaracje zmiennych i nigdy nie musisz się martwić o zamianę `;` na `,` lub wprowadzenie różnic tylko interpunkcyjnych. Możesz również przejrzeć każdą deklarację za pomocą debuggera, zamiast przeskakiwać wszystkie z nich jednocześnie.

    ```javascript
    // złe
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // złe
    // (porównaj z powyższym i spróbuj wykryć błąd)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // dobre
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) Zgrupuj wszystkie swoje `const`y, a następnie zgrupuj wszystkie twoje `let`y.

    > Czemu? Jest to pomocne, gdy później może być konieczne przypisanie zmiennej w zależności od jednej z wcześniej przypisanych zmiennych.

    ```javascript
    // złe
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // złe
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // dobre
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) Przypisz zmienne tam, gdzie ich potrzebujesz, ale umieść je w rozsądnym miejscu.

    > Czemu? `let` oraz `const` mają zasięg blokowy, a nie zasięg funkcjonalny.

    ```javascript
    // złe - niepotrzebne wywołanie funkcji
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // dobre
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```

  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) Nie łącz łańcuchów przypisań zmiennych. eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

    > Czemu? Łańcuchowe przypisania zmiennych tworzy niejawne zmienne globalne.

    ```javascript
    // złe
    (function example() {
      // JavaScript interprets this as
      // let a = ( b = ( c = 1 ) );
      // The let keyword only applies to variable a; variables b and c become
      // global variables.
      let a = b = c = 1;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // 1
    console.log(c); // 1

    // dobre
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // throws ReferenceError
    console.log(c); // throws ReferenceError

    // the same applies for `const`
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) Unikaj stosowania jednoargumentowych inkrementacji i dekrementacji (`++`, `--`). eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > Czemu? Zgodnie z dokumentacją eslint, jednostkowe instrukcje inkrementacji i dekrementacji podlegają automatycznemu wstawianiu średników i mogą powodować ciche błędy przy zwiększaniu lub zmniejszaniu wartości w aplikacji. Bardziej wyraziste jest również mutowanie wartości za pomocą instrukcji takich jak `num + = 1` zamiast `num ++ ` lub `num++`. Nie zezwalanie na jednostkowe instrukcje inkrementacji i dekrementacji zapobiega również przypadkowemu zwiększaniu / dekrementowaniu wartości, co może również powodować nieoczekiwane zachowanie w programach.

    ```javascript
    // złe

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // dobre

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

<a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) Unikaj łamania linii przed lub po `=` w przypisaniu. If your assignment violates [`max-len`](https://eslint.org/docs/rules/max-len.html), surround the value in parens. eslint [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak.html).

    > Czemu? Linie podziału wokół `=` mogą zaciemnić wartość przypisania.

    ```javascript
    // złe
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // złe
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // dobre
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // dobre
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

<a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) Nie zezwalaj na nieużywane zmienne. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > Czemu? Zmienne, które są zadeklarowane i nieużywane nigdzie w kodzie, najprawdopodobniej są błędem z powodu niepełnej refaktoryzacji. Takie zmienne zajmują miejsce w kodzie i mogą prowadzić do zamieszania u czytelników.

    ```javascript
    // złe

    var some_unused_var = 42;

    // Zmienne tylko do zapisu nie są uważane za używane.
    var y = 10;
    y = 5;

    // Odczyt samej modyfikacji nie jest uważany za wykorzystany.
    var z = 0;
    z = z + 1;

    // Nieużywane argumenty funkcji.
    function getX(x, y) {
        return x;
    }

    // dobre

    function getXPlusY(x, y) {
      return x + y;
    }

    var x = 1;
    var y = a + 2;

    alert(getXPlusY(x, y));

    // 'type' jest ignorowany, nawet jeśli nie jest używany, ponieważ ma rodzeństwo właściwości rest.
    // Jest to forma wyodrębnienia obiektu, który pomija określone klucze.
    var { type, ...coords } = data;
    // 'coords' jest teraz obiektem 'data' bez swojej właściwości 'type'.
    ```

**[⬆ powrót do góry](#spis-treści)**

## Hoisting

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) `var` declarations get hoisted to the top of their closest enclosing function scope, their assignment does not. `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone). It’s important to know why [typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // wiemy, że to nie zadziałałoby (zakładając, że
    // nie jest zmienną globalną notDefined)
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // the interpreter is hoisting the variable
    // declaration to the top of the scope,
    // which means our example could be rewritten as:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // używanie const oraz let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) Anonimowe wyrażenia funkcyjne hoistują swoją nazwę zmiennej, ale nie przypisanie funkcji.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="hoisting--named-expressions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expressions) Nazwane wyrażenia funkcyjne hoistują nazwę zmiennej, a nie nazwę funkcji lub body funkcji.

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // to samo dotyczy nazwy funkcji
    // jest taka sama jak nazwa zmiennej.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) Function declarations hoist their name and the function body.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - Aby uzyskać więcej informacji, zobacz [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) od [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ powrót do góry](#spis-treści)**

## Operatory porównania i równości

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) Użyj `===` i `!==` zamiast `==` oraz `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) Instrukcje warunkowe, takie jak instrukcja `if` evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    - **Objects** określa na **true**
    - **Undefined** określa na **false**
    - **Null** określa na **false**
    - **Booleans** określa na **the value of the boolean**
    - **Numbers** określa na **false** jeśli **+0, -0, or NaN**, w innym przypadku **true**
    - **Strings** określa na **false** jeśli pusty string `''`, w innym przypadku **true**

    ```javascript
    if ([0] && []) {
      // true
      // tablica (nawet pusta) jest obiektem, obiekty będą oceniać jako prawdziwe
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) Używaj skrótów dla logicznych wartości, ale wyraźne dla porównania stringów i liczb.
  
    ```javascript
    // złe
    if (isValid === true) {
      // ...
    }

    // dobre
    if (isValid) {
      // ...
    }

    // złe
    if (name) {
      // ...
    }

    // dobre
    if (name !== '') {
      // ...
    }

    // złe
    if (collection.length) {
      // ...
    }

    // dobre
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) Aby uzyskać więcej informacji zobacz [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) od Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) Użyj nawiasów klamrowych, aby utworzyć bloki w klauzulach `case` oraz `default` zawierające deklaracje leksykalne (np. `let`, `const`, `function`, czy `class`). eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

    > Czemu? Deklaracje leksykalne są widoczne w całym bloku `switch`, ale są inicjalizowane tylko wtedy, gdy są przypisane, co dzieje się tylko po osiągnięciu jego `case`. Powoduje to problemy, gdy wiele klauzul `case` próbuje zdefiniować to samo.

    ```javascript
    // złe
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // dobre
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) Ternary nie powinny być zagnieżdżone i zazwyczaj są wyrażeniami jednowierszowymi. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

    ```javascript
    // złe
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // podzielone na 2 oddzielne wyrażenia trójskładnikowe
    const maybeNull = value1 > value2 ? 'baz' : null;

    // lepiej
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // najlepiej
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) Unikaj niepotrzebnych wyrażeń potrójnych. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

    ```javascript
    // złe
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // dobre
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

  <a name="comparison--no-mixed-operators"></a>
  - [15.8](#comparison--no-mixed-operators) Mieszając operatory, umieść je w nawiasach. Jedynym wyjątkiem są standardowe operatory arytmetyczne: `+`, `-`, i `**` ponieważ ich pierwszeństwo jest szeroko rozumiane. Zalecamy otoczyć `/` i `*` w w nawiasach, ponieważ ich pierwszeństwo może być dwuznaczne, gdy są mieszane.
  eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

    > Czemu? Poprawia to czytelność i wyjaśnia zamiar programisty.

    ```javascript
    // złe
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // złe
    const bar = a ** b - 5 % d;

    // złe
    // one may be confused into thinking (a || b) && c
    if (a || b && c) {
      return d;
    }

    // złe
    const bar = a + b / c * d;

    // dobre
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // dobre
    const bar = a ** b - (5 % d);

    // dobre
    if (a || (b && c)) {
      return d;
    }

    // dobre
    const bar = a + (b / c) * d;
    ```

**[⬆ powrót do góry](#spis-treści)**

## Bloki

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) Używaj nawiasów klamrowych ze wszystkimi wielowierszowymi blokami. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

    ```javascript
    // złe
    if (test)
      return false;

    // dobre
    if (test) return false;

    // dobre
    if (test) {
      return false;
    }

    // złe
    function foo() { return false; }

    // dobre
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) Jeśli używasz wielowierszowe bloki z `if` i `else`, umieść `else` w tej samej linii co nawias zamykający bloku `if`. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

    ```javascript
    // złe
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // dobre
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  <a name="blocks--no-else-return"></a><a name="16.3"></a>
  - [16.3](#blocks--no-else-return) Jeśli blok `if` zawsze wykonuje instrukcję `return`, kolejny blok `else` jest niepotrzebny. `return` w bloku `else if` po bloku `if`, który zawiera `return`, można podzielić na wiele bloków `if`. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // złe
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // złe
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // złe
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // dobre
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // dobre
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // dobre
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Control Statements

  <a name="control-statements"></a>
  - [17.1](#control-statements) In case your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

    > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

    ```javascript
    // złe
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // złe
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // złe
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // złe
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // dobre
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // dobre
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // dobre
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

  <a name="control-statement--value-selection"></a><a name="control-statements--value-selection"></a>
  - [17.2](#control-statements--value-selection) Nie używaj operatorów wyboru zamiast instrukcji sterujących.

    ```javascript
    // złe
    !isRunning && startRunning();

    // dobre
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Komentarze

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [18.1](#comments--multiline) Użyj `/** ... */` dla wielowierszowych komentarzy.

    ```javascript
    // złe
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // dobre
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [18.2](#comments--singleline) Użyj `//` dla komentarzy w pojedynczej linii. Umieść komentarze w jednym wierszu w nowym wierszu nad tematem komentarza. Umieść pusty wiersz przed komentarzem, chyba że znajduje się on w pierwszym wierszu bloku.

    ```javascript
    // złe
    const active = true;  // is current tab

    // dobre
    // is current tab
    const active = true;

    // złe
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // dobre
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) Rozpocznij wszystkie komentarze spacją, aby ułatwić czytanie. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // złe
    // is current tab
    const active = true;

    // dobre
    // is current tab
    const active = true;

    // złe
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // dobre
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [18.4](#comments--actionitems) Poprzedź swoje komentarze za pomocą `FIXME` lub `TODO` co pomaga innym programistom w szybkim zrozumieniu, czy wskazujesz problem, który należy ponownie zgłosić, lub sugerujesz rozwiązanie problemu, który należy wdrożyć. Różnią się one od zwykłych komentarzy, ponieważ można je wykonać. Działania są `FIXME: -- need to figure this out` lub `TODO: -- need to implement`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [18.5](#comments--fixme) Użyj `// FIXME:` aby opisywać problemy.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn’t use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [18.6](#comments--todo) Użyj `// TODO:` aby opisywać rozwiązania problemów.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Białe spacje

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [19.1](#whitespace--spaces) Użyj miękkich tabulatorów (spacji) ustawionych na 2 spacje. eslint: [`indent`](https://eslint.org/docs/rules/indent.html)

    ```javascript
    // złe
    function foo() {
    ∙∙∙∙let name;
    }

    // złe
    function bar() {
    ∙let name;
    }

    // dobre
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [19.2](#whitespace--before-blocks) Umieść 1 spację przed nawiasem rozpoczynającym. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)

    ```javascript
    // złe
    function test(){
      console.log('test');
    }

    // dobre
    function test() {
      console.log('test');
    }

    // złe
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // dobre
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [19.3](#whitespace--around-keywords) Umieść 1 spację przed nawiasem otwierającym w instrukcjach sterujących (`if`, `while` etc.). Nie umieszczaj spacji między listą argumentów a nazwą funkcji w wywołaniach funkcji i deklaracjach. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)

    ```javascript
    // złe
    if(isJedi) {
      fight ();
    }

    // dobre
    if (isJedi) {
      fight();
    }

    // złe
    function fight () {
      console.log ('Swooosh!');
    }

    // dobre
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [19.4](#whitespace--infix-ops) Set off operators with spaces. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)

    ```javascript
    // złe
    const x=y+5;

    // dobre
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) Zakończ pliki pojedynczym znakiem nowej linii. eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

    ```javascript
    // złe
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // złe
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // dobre
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [19.6](#whitespace--chains) Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
    emphasizes that the line is a method call, not a new statement. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // złe
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // złe
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // dobre
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // złe
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // dobre
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // dobre
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [19.7](#whitespace--after-blocks) Pozostaw puste wiersze po blokach i przed następną instrukcją.

    ```javascript
    // złe
    if (foo) {
      return bar;
    }
    return baz;

    // dobre
    if (foo) {
      return bar;
    }

    return baz;

    // złe
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // dobre
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // złe
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // dobre
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [19.8](#whitespace--padded-blocks) Nie wypełniaj bloków pustymi liniami. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)

    ```javascript
    // złe
    function bar() {

      console.log(foo);

    }

    // złe
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // złe
    class Foo {

      constructor(bar) {
        this.bar = bar;
      }
    }

    // dobre
    function bar() {
      console.log(foo);
    }

    // dobre
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--no-multiple-blanks"></a>
  - [19.9](#whitespace--no-multiple-blanks) Nie używaj wielu pustych linii do uzupełnienia kodu. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // złe
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;


        this.email = email;


        this.setAge(birthday);
      }


      setAge(birthday) {
        const today = new Date();


        const age = this.getAge(today, birthday);


        this.age = age;
      }


      getAge(today, birthday) {
        // ..
      }
    }

    // dobre
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;
        this.email = email;
        this.setAge(birthday);
      }

      setAge(birthday) {
        const today = new Date();
        const age = getAge(today, birthday);
        this.age = age;
      }

      getAge(today, birthday) {
        // ..
      }
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [19.10](#whitespace--in-parens) Nie dodawaj spacji w nawiasach. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)

    ```javascript
    // złe
    function bar( foo ) {
      return foo;
    }

    // dobre
    function bar(foo) {
      return foo;
    }

    // złe
    if ( foo ) {
      console.log(foo);
    }

    // dobre
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [19.11](#whitespace--in-brackets) Nie dodawaj spacji w nawiasach. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)

    ```javascript
    // złe
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // dobre
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [19.12](#whitespace--in-braces) Dodaj spacje w nawiasach klamrowych. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)

    ```javascript
    // złe
    const foo = {clark: 'kent'};

    // dobre
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [19.13](#whitespace--max-len) Unikaj linii kodu dłuższych niż 100 znaków (w tym białych znaków). Uwaga: na [powyżej](#strings--line-length), długie stringi są zwolnione z tej zasady i nie powinny być dzielone. eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

    > Czemu? Zapewnia to czytelność i łatwość konserwacji.

    ```javascript
    // złe
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // złe
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // dobre
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // dobre
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

  <a name="whitespace--block-spacing"></a>
  - [19.14](#whitespace--block-spacing) Require consistent spacing inside an open block token and the next token on the same line. This rule also enforces consistent spacing inside a close block token and previous token on the same line. eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // złe
    function foo() {return true;}
    if (foo) { bar = 0;}

    // dobre
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.15](#whitespace--comma-spacing) Unikaj spacji przed przecinkami i wymagaj spacji po przecinkach. eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // złe
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // dobre
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.16](#whitespace--computed-property-spacing) Enforce spacing inside of computed property brackets. eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

    ```javascript
    // złe
    obj[foo ]
    obj[ 'foo']
    var x = {[ b ]: a}
    obj[foo[ bar ]]

    // dobre
    obj[foo]
    obj['foo']
    var x = { [b]: a }
    obj[foo[bar]]
    ```

  <a name="whitespace--func-call-spacing"></a>
  - [19.17](#whitespace--func-call-spacing) Unikaj spacji między funkcjami i ich wywołaniami. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // złe
    func ();

    func
    ();

    // dobre
    func();
    ```

  <a name="whitespace--key-spacing"></a>
  - [19.18](#whitespace--key-spacing)Wymuszaj odstępy między kluczami a wartościami we właściwościach literału obiektu. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // złe
    var obj = { foo : 42 };
    var obj2 = { foo:42 };

    // dobre
    var obj = { foo: 42 };
    ```

  <a name="whitespace--no-trailing-spaces"></a>
  - [19.19](#whitespace--no-trailing-spaces) Unikaj spacji na końcu linii. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.20](#whitespace--no-multiple-empty-lines) Unikaj wielu pustych linii, zezwalaj tylko na jedną nową linię na końcu plików i unikaj nowej linii na początku plików. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // złe - wiele pustych linii
    var x = 1;


    var y = 2;

    // złe - 2+ nowe linie na końcu pliku
    var x = 1;
    var y = 2;


    // złe - 1+ nowa linia(e) na początku pliku

    var x = 1;
    var y = 2;

    // dobre
    var x = 1;
    var y = 2;

    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ powrót do góry](#spis-treści)**

## Przecinki

  <a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) Leading commas: **Nope.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)

    ```javascript
    // złe
    const story = [
        once
      , upon
      , aTime
    ];

    // dobre
    const story = [
      once,
      upon,
      aTime,
    ];

    // złe
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // dobre
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [20.2](#commas--dangling) Additional trailing comma: **Yup.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

    > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don’t have to worry about the [trailing comma problem](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) in legacy browsers.

    ```diff
    // złe - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // dobre - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // złe
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // dobre
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // złe
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // dobre
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // dobre (note that a comma must not appear after a "rest" element)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // złe
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // dobre
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // dobre (note that a comma must not appear after a "rest" element)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ powrót do góry](#spis-treści)**

## Średniki

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [21.1](#semicolons--required) **Yup.** eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

    > Czemu? Gdy JavaScript napotyka podział wiersza bez średnika, używa zestawu reguł o nazwie [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) aby ustalić, czy powinien on traktować podział wiersza jako koniec instrukcji i (jak sama nazwa wskazuje) umieścić średnik w kodzie przed podziałem wiersza, jeśli tak uważa. ASI zawiera jednak kilka ekscentrycznych zachowań, a twój kod się zepsuje, jeśli JavaScript źle interpretuje podział linii. Reguły te staną się bardziej skomplikowane, gdy nowe funkcje staną się częścią JavaScript. Jawne zakończenie instrukcji i konfiguracja linijki w celu wychwycenia brakujących średników pomoże ci uniknąć problemów.

    ```javascript
    // złe - raises exception
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // złe - raises exception
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // złe - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // dobre
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // dobre
    const reaction = "No! That’s impossible!";
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // dobre
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [Read more](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ powrót do góry](#spis-treści)**

## Type Casting & Coercion

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [22.1](#coercion--explicit) Perform type coercion at the beginning of the statement.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [22.2](#coercion--strings) Strings: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // złe
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // złe
    const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

    // złe
    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

    // dobre
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const inputValue = '4';

    // złe
    const val = new Number(inputValue);

    // złe
    const val = +inputValue;

    // złe
    const val = inputValue >> 0;

    // złe
    const val = parseInt(inputValue);

    // dobre
    const val = Number(inputValue);

    // dobre
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](https://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you’re doing.

    ```javascript
    // dobre
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](https://es5.github.io/#x4.3.19), but bitshift operations always return a 32-bit integer ([source](https://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [22.6](#coercion--booleans) Booleans: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // złe
    const hasAge = new Boolean(age);

    // dobre
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ powrót do góry](#spis-treści)**

## Konwencje nazewnictwa

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [23.1](#naming--descriptive) Unikaj nazw jednoliterowych. Podaj swoje nazwy w sposób opisowy. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // złe
    function q() {
      // ...
    }

    // dobre
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [23.2](#naming--camelCase) Użyj camelCase podczas nadawania nazw dla obiektów, funkcji, i instancji. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

    ```javascript
    // złe
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // dobre
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [23.3](#naming--PascalCase) Użyj PascalCase tylko podczas nazywania konstruktorów lub klas. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

    ```javascript
    // złe
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // dobre
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [23.4](#naming--leading-underscore) Do not use trailing or leading underscores. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)

    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won’t count as breaking, or that tests aren’t needed. tl;dr: if you want something to be “private”, it must not be observably present.

    ```javascript
    // złe
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // dobre
    this.firstName = 'Panda';

    // dobre, in environments where WeakMaps are available
    // see https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) Don’t save references to `this`. Use arrow functions or [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    ```javascript
    // złe
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // złe
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // dobre
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [23.6](#naming--filename-matches-export) A base filename should exactly match the name of its default export.

    ```javascript
    // file 1 contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // file 2 contents
    export default function fortyTwo() { return 42; }

    // file 3 contents
    export default function insideDirectory() {}

    // in some other file
    // złe
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // złe
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // dobre
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) Use camelCase when you export-default a function. Your filename should be identical to your function’s name.

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) Acronyms and initialisms should always be all uppercased, or all lowercased.

    > Why? Names are for readability, not to appease a computer algorithm.

    ```javascript
    // złe
    import SmsContainer from './containers/SmsContainer';

    // złe
    const HttpRequests = [
      // ...
    ];

    // dobre
    import SMSContainer from './containers/SMSContainer';

    // dobre
    const HTTPRequests = [
      // ...
    ];

    // also good
    const httpRequests = [
      // ...
    ];

    // best
    import TextMessageContainer from './containers/TextMessageContainer';

    // best
    const requests = [
      // ...
    ];
    ```

  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) You may optionally uppercase a constant only if it (1) is exported, (2) is a `const` (it can not be reassigned), and (3) the programmer can trust it (and its nested properties) to never change.

    > Why? This is an additional tool to assist in situations where the programmer would be unsure if a variable might ever change. UPPERCASE_VARIABLES are letting the programmer know that they can trust the variable (and its properties) not to change.
    - What about all `const` variables? - This is unnecessary, so uppercasing should not be used for constants within a file. It should be used for exported constants however.
    - What about exported objects? - Uppercase at the top level of export (e.g. `EXPORTED_OBJECT.key`) and maintain that all nested properties do not change.

    ```javascript
    // złe
    const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

    // złe
    export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

    // złe
    export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';

    // ---

    // allowed but does not supply semantic value
    export const apiKey = 'SOMEKEY';

    // better in most cases
    export const API_KEY = 'SOMEKEY';

    // ---

    // złe - unnecessarily uppercases key while adding no semantic value
    export const MAPPING = {
      KEY: 'value'
    };

    // dobre
    export const MAPPING = {
      key: 'value'
    };
    ```

**[⬆ powrót do góry](#spis-treści)**

## Accessors

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [24.1](#accessors--not-required) Accessor functions for properties are not required.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use `getVal()` and `setVal('hello')`.

    ```javascript
    // złe
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // dobre
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [24.3](#accessors--boolean-prefix) If the property/method is a `boolean`, use `isVal()` or `hasVal()`.

    ```javascript
    // złe
    if (!dragon.age()) {
      return false;
    }

    // dobre
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [24.4](#accessors--consistent) It’s okay to create `get()` and `set()` functions, but be consistent.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ powrót do góry](#spis-treści)**

## Events

  <a name="events--hash"></a><a name="24.1"></a>
  - [25.1](#events--hash) When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass an object literal (also known as a "hash") instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // złe
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // do something with listingID
    });
    ```

    prefer:

    ```javascript
    // dobre
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingID
    });
    ```

  **[⬆ powrót do góry](#spis-treści)**

## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) Prefix jQuery object variables with a `$`.

    ```javascript
    // złe
    const sidebar = $('.sidebar');

    // dobre
    const $sidebar = $('.sidebar');

    // dobre
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) Cache jQuery lookups.

    ```javascript
    // złe
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // dobre
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [26.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // złe
    $('ul', '.sidebar').hide();

    // złe
    $('.sidebar').find('ul').hide();

    // dobre
    $('.sidebar ul').hide();

    // dobre
    $('.sidebar > ul').hide();

    // dobre
    $sidebar.find('ul').hide();
    ```

**[⬆ powrót do góry](#spis-treści)**

## ECMAScript 5 Compatibility

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) Refer to [Kangax](https://twitter.com/kangax/)’s ES5 [compatibility table](https://kangax.github.io/es5-compat-table/).

**[⬆ powrót do góry](#spis-treści)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) This is a collection of links to the various ES6+ features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#classes--constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Exponentiation Operator](#es2016-properties--exponentiation-operator)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) Do not use [TC39 proposals](https://github.com/tc39/proposals) that have not reached stage 3.

    > Why? [They are not finalized](https://tc39.github.io/process-document/), and they are subject to change or to be withdrawn entirely. We want to use JavaScript, and proposals are not JavaScript yet.

**[⬆ powrót do góry](#spis-treści)**

## Standard Library

  The [Standard Library](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)
  contains utilities that are functionally broken but remain for legacy reasons.

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) Use `Number.isNaN` instead of global `isNaN`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? The global `isNaN` coerces non-numbers to numbers, returning true for anything that coerces to NaN.
    > If this behavior is desired, make it explicit.

    ```javascript
    // złe
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // dobre
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) Use `Number.isFinite` instead of global `isFinite`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? The global `isFinite` coerces non-numbers to numbers, returning true for anything that coerces to a finite number.
    > If this behavior is desired, make it explicit.

    ```javascript
    // złe
    isFinite('2e3'); // true

    // dobre
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ powrót do góry](#spis-treści)**

## Testowanie

  <a name="testing--yup"></a><a name="28.1"></a>
  - [30.1](#testing--yup) **Yup.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [30.2](#testing--for-real) **No, but seriously**:
    - Whichever testing framework you use, you should be writing tests!
    - Strive to write many small pure functions, and minimize where mutations occur.
    - Be cautious about stubs and mocks - they can make your tests more brittle.
    - We primarily use [`mocha`](https://www.npmjs.com/package/mocha) and [`jest`](https://www.npmjs.com/package/jest) at Airbnb. [`tape`](https://www.npmjs.com/package/tape) is also used occasionally for small, separate modules.
    - 100% test coverage is a good goal to strive for, even if it’s not always practical to reach it.
    - Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ powrót do góry](#spis-treści)**

## Wydajność

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost/12)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/164)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat/38)
  - [Are JavaScript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ powrót do góry](#spis-treści)**

## Resources

**Learning ES6+**

  - [Latest ECMA spec](https://tc39.github.io/ecma262/)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Read This**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Narzędzia**

  - Code Style Linters
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
  - [Google JavaScript Style Guide (Old)](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Książki**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X) - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don’t Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogi**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasty**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ powrót do góry](#spis-treści)**

## In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **123erfasst**: [123erfasst/javascript](https://github.com/123erfasst/javascript)
  - **3blades**: [3Blades](https://github.com/3blades)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Adult Swim**: [adult-swim/javascript](https://github.com/adult-swim/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avalara**: [avalara/javascript](https://github.com/avalara/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **BashPros**: [BashPros/javascript](https://github.com/BashPros/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk](https://github.com/Bisk/)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Cerner**: [Cerner](https://github.com/cerner/)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **Coeur d'Alene Tribe**: [www.cdatribe-nsn.gov](https://www.cdatribe-nsn.gov)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Drupal**: [www.drupal.org](https://www.drupal.org/project/drupal)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Expensify** [Expensify/Style-Guide](https://github.com/Expensify/Style-Guide/blob/master/javascript.md)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia](https://github.com/gawkermedia/)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **GreenChef**: [greenchef/javascript](https://github.com/greenchef/javascript)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Grupo-Abraxas**: [Grupo-Abraxas/javascript](https://github.com/Grupo-Abraxas/javascript)
  - **Happeo**: [happeo/javascript](https://github.com/happeo/javascript)
  - **Honey**: [honeyscience/javascript](https://github.com/honeyscience/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **Huballin**: [huballin](https://github.com/huballin/)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://github.com/kesne/jeopardy-bot/blob/master/STYLEGUIDE.md)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **Kaplan Komputing**: [kaplankomputing/javascript](https://github.com/kaplankomputing/javascript)
  - **KickorStick**: [kickorstick](https://github.com/kickorstick/)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **LEINWAND**: [LEINWAND/javascript](https://github.com/LEINWAND/javascript)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **ModCloth**: [modcloth/javascript](https://github.com/modcloth/javascript)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://github.com/moneyadviceservice/javascript)
  - **Muber**: [muber](https://github.com/muber/)
  - **National Geographic**: [natgeo](https://github.com/natgeo/)
  - **Nimbl3**: [nimbl3/javascript](https://github.com/nimbl3/javascript)
  - **NullDev**: [NullDevCo/JavaScript-Styleguide](https://github.com/NullDevCo/JavaScript-Styleguide)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Pier 1**: [Pier1/javascript](https://github.com/pier1/javascript)
  - **Qotto**: [Qotto/javascript-style-guide](https://github.com/Qotto/javascript-style-guide)
  - **Razorfish**: [razorfish/javascript-style-guide](https://github.com/razorfish/javascript-style-guide)
  - **reddit**: [reddit/styleguide/javascript](https://github.com/reddit/styleguide/tree/master/javascript)
  - **React**: [facebook.github.io/react/contributing/how-to-contribute.html#style-guide](https://facebook.github.io/react/contributing/how-to-contribute.html#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **Sainsbury’s Supermarkets**: [jsainsburyplc](https://github.com/jsainsburyplc)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://github.com/seekingalpha/javascript-style-guide)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload](https://github.com/springload/)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **Terra**: [terra](https://github.com/cerner?utf8=%E2%9C%93&q=terra&type=&language=)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **Tomify**: [tomprats](https://github.com/tomprats)
  - **Traitify**: [traitify/eslint-config-traitify](https://github.com/traitify/eslint-config-traitify)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **UrbanSim**: [urbansim](https://github.com/urbansim/)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ powrót do góry](#spis-treści)**

## Tłumaczenie

  Ten przewodnik po stylach jest również dostępny w innych językach:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [lin-123/javascript](https://github.com/lin-123/javascript)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [eraycetinay/javascript](https://github.com/eraycetinay/javascript)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [dangkyokhoang/javascript-style-guide](https://github.com/dangkyokhoang/javascript-style-guide)
  - ![🇵🇱](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [mbiesiad/javascript-style-guide](https://github.com/mbiesiad/javascript)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chatuj z nami na temat JavaScript

  - Znajdź nas na [gitter](https://gitter.im/airbnb/javascript).

## Współtwórcy

  - [Zobacz Współtwórców](https://github.com/airbnb/javascript/graphs/contributors)

## Licencja

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ powrót do góry](#spis-treści)**

## Poprawki

Zachęcamy do forka tego przewodnika i zmiany zasad w celu dopasowania do przewodnika po stylu dla twojego zespołu. Poniżej możesz wymienić kilka poprawek do przewodnika po stylach. Umożliwia to okresową aktualizację przewodnika po stylu bez konieczności rozwiązywania konfliktów mergowania.

# };
