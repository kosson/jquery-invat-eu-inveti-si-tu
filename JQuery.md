# JQuery învăț eu, înveți și tu

## Un manual pentru cei grăbiți

de Nicolaie Constantinescu

## Introducere

Este o bibliotecă utilă selectării rapide și a dinamizării elementelor. Marca bibliotecii de cod este semnul `$`, care este un alias pentru obiectul JQuery.

```javascript
$(function () {
    // codul jquery
})
```

Apelarea lui `$()` are drept efect instanțierea obiectului jQuery. Pasarea unei funcții la momentul instanțierii, permite programarea apelurilor de funcții pentru a fi încărcate la momentul în care este încărcat DOM-ul.

Pentru a face uz de noua sintaxă JavaScript, vom putea reformula expresia dată drept exemplu.

```javascript
$(() => {
  // codul jquery
});
```

Funcția care instanțiază jQuery, poate accepta drept argumente alte funcții declarate deja.

```javascript
function adaugaEvidentiator()  {
  $('div.ceva').addClass('subliniaza');
}
$(adaugaEvidentiator);
```

## 1. Afișarea și ascunderea elementelor

### 1.1 Ascunde elemente

Pentru ascunderea elementelor, folosește metoda `hide()`. Ascunderea elementului poate fi animată, dacă metodei i se dă valoarea în milisecunde: `hide(2000)`.

### 1.2 Apariție elemente

Pentru a face un element să apară, folosește metoda `show()`. Apariția poate fi animată dacă i se oferă un parametru care menționează durata în milisecunde: `show(2000)`.

### 1.3 Toggle elemente

Pentru a realiza apariția și ascunderea elementelor, se va folosi metoda `toggle()`.

## 2. Animații - modele

### 2.1 Fade pe elemente

Metode folosite pentru a realiza un efect de fade:
- `fadeTo(3000)` sau `fadeTo('slow')`,
- `fadeIn(2000, 0.3)` - specifici timpul și valoarea canalului alpha (transparența),
- `fadeOut(4000)`
- `fadeToggle()`

```javascript
  $(".red-box").fadeTo(3000, 0.2);
  $('.green-box').fadeIn(3000);
  $('.blue-box').fadeTo(3000, 0.5);
  $('.blue-box').fadeToggle();
  $('.blue-box').fadeToggle();
```

#### 2.1.1 Metoda `fadeOut()`

Metoda, va reduce opacitatea (`opacity`) elementului la `0` și apoi va seta `display` la valoarea `none`.

#### 2.1.2 Metoda `fadeIn()`

Metoda va seta valoarea `display` la `block`, făcând elementul să apară. Va seta și transparența la valoarea specificată, iar dacă aceasta nu este, va fi setată la `1`, însemnând că elementul este vizibil complet.

#### 2.1.3 Metoda `fadeTo()`

Metoda va seta elementul la o valoare a transparenței menționată în al doilea parametru între `0` și `1`.

#### 2.1.4 Metoda `fadeToggle()`

Pur și simplu realizează opusul setărilor pentru un anumit element.

#### 2.1.5 Temporizarea animațiilor prin callback-uri

Metodele prezentare anterior acceptă și un al treilea argument care poate fi o funcție cu rol de callback. Callback-ul va fi executat de îndată ce animația s-a încheiat.

```javascript
  $(".red-box").fadeTo(3000, 0.2, function () {
      console.log('Am încheiat animația');
  });
```

### 2.2 Efecte de sliding

#### 2.2.1 Metoda `slideUp()`

Este o metodă care are un efect similar celui realizat prin aplicarea metodei `fadeOut()`. Ceea ce se realizează prin aplicarea metodei, este eliminarea unui element prin translarea pe verticală.

Proprietăți CSS afectate:

- `overflow: hidden`
- `height` scade continuu până la valoarea `0`,
- `padding-top` se modifică valoarea, scăzând la `0`,
- `padding-bottom` se modifică valoarea, scăzând la `0`,
- `margin-bottom` se modifică valoarea, scăzând la `0`,

La final, elementul va fi scos din normal flow, valoarea lui `display`, fiind setată la `none`.

#### 2.2.2 Metoda `slideDown()`

Efectul realizat este cel opus lui `slideup`, ceea ce conduce la apariția elementului pornind cu latura superioară.

#### 2.2.3 Metoda `slideToggle()`

Dacă elementul este ascuns, îl va introduce prin efect de *slideDown*, iar dacă este vizibil, îl va ascunde cu *slideUp*.

#### 2.2.4 Metoda `animate()`

Metoda `animate` primește un obiect în care specifici proprietățile CSS pe care dorești să le animezi.

```javascript
$('.element-vizat').animate({
    "margin-left": "200px",
    "height": "50px",
    "width": "50px",
    "margin-top": "25px"
}, 2000, 'linear');
```

Ceea ce se va petrece este o glisare a elementelor din stânga, în cazul nostru pornind de la valoarea existentă, până la valoarea pasată în obiect.

Pentru a lucra cu valorile existente, poți folosi și operatorii `+=` și `-=`: `"margin-left": "+=200px"`.

Al doilea prametru pasat este timpul în care animația va fi performată. Valoarea din oficiu este 400 de milisecunde.

Se paote adăuga un al treilea argument metodei, care este string și definește modul în care se face translația, din punct de vedere al accelerării și decelerării pe ecran.

Adăugând proprietăți în obiectul pasat ca prim argument metodei `animate()`, poți anima orice proprietate CSS dorită. Poți modifica opacitate, etc.

În cazul în care dorești, JQuery pune la dispoziție proprii identificatori pentru proprietățile CSS care vor fi animate.

```javascript
$('.element-vizat').animate({
    marginLeft: "200px",
    height: "50px",
    width: "50px",
    marginTop: "25px",
    opacity: 0.5
}, 2000, 'linear');
```

#### 2.2.5 Animații înlănțuite - metoda `delay()`

Animațiile pot urma o logică. Un eveniment de animație poate urma altuia.

Pentru a realiza o posibilă logică, se va folosi metoda `delay()` care acceptă valoarea de timp dată evenimentului de animație anterior, iar dacă mai era unul anterior, vei adăuga și valoarea aceluia, ș.a.m.d.

```javascript
  $(".red-box").fadeTo(3000, 0.2);
  $('.green-box').delay(3000).fadeTo(3000, 0.4);
  $('.blue-box').fadeTo(3000, 0.8);
```

Pentru a realiza o înlănțuire a momentelor de animație, se poate recurge și la folosirea funcțiilor cu rol de callback.

```javascript
  $(".red-box").fadeTo(3000, 0.2, function () {
      console.log('Am încheiat prima animație');
      $('.green-box').fadeTo(3000, 0.4, function () {
          console.log('Începe a doua animație după prima);
          $('.green-box').delay(3000).fadeTo(3000, 0.4);
      });
  });
```

Pentru a dezvolta un mic exemplu, vom crea un mic ecran de întâmpinare, care este un element ce apare pe tot ecranul.

```html
<div class="lightbox">
    <p>Acesta este conținutul pentru exemplificarea unui lightbox</p>
    <form action="">
        <input type="text" name="" id="">
        <button type="submit"></button>
    </form>
</div>
<script>
$('.lightbox').delay(500).fadeIn(4000);
</script>
```

## 3. Selectarea elementelor

### 3.1 Selectarea tuturor elementelor corespondente unui tag

Pentru a selecta toate elementele care sunt de un anumit tag, se va folosi selectorul corespondent respectivului tag `$('p')`.

### 3.2 Modificarea proprietăților CSS

Poți modifica proprietățile CSS folosind metoda `css()`.

```javascript
$(function(){
  $('p').css('background-color', 'rgba(120, 120, 230, 0.6)');
  $('p:first').css('background-color', 'rgba(120, 120, 230, 0.6)');
  $('p:last').css('background-color', 'rgba(120, 120, 230, 0.6)');
  $('p:even').css('background-color', 'rgba(120, 120, 230, 0.6)');
  $('p:odd').css('background-color', 'rgba(120, 120, 230, 0.6)');
  $('input[type="text"]').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('input:text').css('background-color', 'rgba(130, 130, 130, 0.6)'); // toate text
  $('input:password').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('input:checkbox').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('input:radio').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('input:checked').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('input:selected').css('background-color', 'rgba(130, 130, 130, 0.6)');
  $('p, h1').css('color', 'rgba(210, 120, 230, 0.7)');
});
```

### 3.3 Traversarea DOM-ului

JQuery permite căutarea recursivă în structura arborescentă a DOM-ului pentru a identifica elementele căutate sau tagurile, dacă se dorește.

#### 3.3.1 Metoda `find()`

Metoda find se comportă ca un mecanism de căutare într-o structură DOM, indiferent de dimensiunea sa. Drept parametru i se poate pasa un selector.

```javascript
$(function () {
  $('#lista').find('li').css('background-color', 'rgba(110, 120, 130, 0.7)');
});
```

Metodei i se poate face chainin cu transformările dorite.

#### 3.3.2 Metoda `children()`

Această metodă selectează copiii unui element țintit.

```javascript
$('#lista').children('li').css('color', 'red');
```

#### 3.3.3 Metoda `parents()`

Această metodă oferă posibilitatea de a parcurge structurile părinte ale unui element țintit. Dacă pasezi ca string numele unui selector, doar acele elemente din părinți vor fi afectate.

```javascript
$('#lista').parents('div').css('background-color', 'salmon');
```

#### 3.3.4 Metoda `parent()`

Această metodă indică direct un unic selector părinte țintit.

#### 3.3.5 Metoda `siblings()`

Această metodă țintește toate elementele de pe aceeași ramură a arborelui DOM, dar exceptează pe cel asupra căruia s-a apelat metoda.

Metodei i se poate pasa un argument care menționează care selector dintre elementele de pe aceeași ramură este țintit.

```javascript
$('#lista').siblings('p').css('color','green');
```

Pentru a selecta elementele siblings de deasupra elementului țintit, JQuery oferă un selector special `:header`.

```javascript
$('#lista').siblings(':header').css('color', 'salmon');
```

#### 3.3.6 Metodele `prev()` și `next()`

Aceste metode permit o selecție rapidă a elementelor adiacente celui țintit.

#### 3.3.7 Metoda `first()`

Această metodă reduce setul de elemente găsit la primul element din set. Metoda nu acceptă argumente.

```javascript
$( "li" ).first().css( "background-color", "red" );
```

#### 3.3.8 Metoda `last()`

Dintr-un set de element găsite conform criteriilor de selecție, va fi capturat ultimul.

```javascript
$( "p span" ).last().addClass( "highlight" );
```

#### 3.3.9 Metoda `closest()`

Este o metodă care caută într-un obiect JQuery care reprezintă un set de elemente DOM și construiește un nou obiect din elementele care se potrivesc criteriilor. Metoda se aseamănă cu `.parents()`, dar prezintă particularități. Spre deosebire de `.parent()`, care începe cu elementul părinte, `.closest()` pornește chiar cu însuși elementul.

Căutarea se oprește în momentul în care este găsit elementul/ele care corespund/e criteriilor de căutare.

```javascript
$( "li.item-a" )
  .closest( "li" )
  .css( "background-color", "red" );
```

La nevoie poate fi pasat și un obiect DOM, care să fie considerat context de căutare.

```javascript
var listItemII = document.getElementById( "ii" );
$( "li.item-a" )
  .closest( "ul", listItemII )
  .css( "background-color", "red" );
$( "li.item-a" )
  .closest( "#one", listItemII )
  .css( "background-color", "green" );
```

Metoda poate fi folosită și pentru executarea unui eveniment care a fost delegat.

```javascript
$( document ).on( "click", function( event ) {
  $( event.target ).closest( "li" ).toggleClass( "highlight" );
});
```

Poți pasa chiar un obiect.

```javascript
var listElements = $( "li" ).css( "color", "blue" );
$( document ).on( "click", function( event ) {
  $( event.target ).closest( listElements ).toggleClass( "highlight" );
});
```

### 3.4 Filtrare elemente

JQuery pune la dispoziție instrumente capabile să facă o filtrare a elementelor.

#### 3.4.1 Metoda `filter()`

Este metoda necesară filtrării elementelor după anumite criterii.

```javascript
$('#lista').children('li').filter(':even').css('color', 'blue');
```

Metoda `filter()` poate primi drept argument o funcție care poate prelucra fiecare element din lista elementelor țintite. Această funcție se comportă ca un `foreach'.

```javascript
$('li').filter(function(indexElem){
  return indexElem % 3 === 0; // selectează toate elementele === 1 pe cele odd, === 2 pe cele even
}).css('color', 'red');
```

Pentru elementele pentru care funcția returnează `true`, se va aplica ceea ce urmează în lanț.

#### 3.4.2 Metodele `first()` și `last()`

Această metodă va selecta primul element din setul țintit.

```javascript
$('#lista').first().css('color', 'red');
```

Pentru a selecta ultimul element din setul țintit, se va folosi metoda `last()`.

#### 3.4.3 Metoda `eq()`

Această metodă este folosită pentru a ținti un element din setul adus de selector.

```javascript
$('#lista').eq(1).css('color', 'red');
```

De exemplu, pentru `eq` valoarea `0` selectează primul element din set, `1` pe a doua ș.a.m.d.

O valoare negativă înseamnă selectarea unei valori de la coada listei elementelor selectate înapoi. De exemplu, `eq(-2)` înseamnă al doilea element din coadă.

#### 3.4.4 Metoda `not()`

Această metodă va ignora ceea ce este specificat prin argument.

```javascript
$('li').not(':first').css('color', 'green');
$('li').not('#lista ul li').css('color', 'green');
```

Precum în cazul `filter()`, și metoda `not()` acceptă o funcție callback, care se aplică fiecărui element din cele care au fost țintite.

### 3.5 Iterare elemente și lucru cu seturi de elemente

#### 3.5.1 Metoda `each()`

Această metodă este similară lui `forEach()`. Metoda va primi drept argument o funcție cu rol de callback, care se va aplica pe fiecare element din setul vizat.

Metoda poate primi două argumente: un contor cu ajutorul căruia să putem ține evidența numărului de iterații parcurse și obiectul JQuery asupra căruia se va opera în funcția callback.

```javascript
var $ancora = $('<div id="ancora"></div>');
$('span.undeva').each((contor, obiectul) => {
    $(`<sup>${contor + 1}</sup>`)
    $(obiectul).appendTo($ancora).wrap('<section></section>');
});
```

## 4. Crearea elementelor și manipularea DOM-ului

Crearea elementelor în JQuery este o simplă operațiune de a introduce drept argument funcției un string, care este fragmentul de cod HTML ce trebuie introdus în pagină.

```javascript
$('<p>Un fragment de cod</p>')
```

În acest moment avem un fragment de HTML, dar trebuie menționat locul în care se va face inserarea.

```javascript
$(() => {
    $('<p>De inserat</p>').appendBefore('div.ceva p');
});
```

Pentru a stabili rapid câteva repere în manipularea DOM-ului, JQuery oferă câteva metode pe care le putem împărți după utilitate. Știm deja că metoda generală `$()` permite crearea de elemente HTML.

Pentru a insera noi elemente, în toate elementele care au fost găsite conform selectorului, vor fi folosite următoarele metode.

- `append()`
- `appendTo()`
- `prepend()`
- `prependTo()`

Pentru a insera elemente adiacent elementului vizat, se vor folosi următoarele metode:

- `after()`
- `insertAfter()`
- `before()`
- `insertBefore()`

Pentru a **împături** fiecare element găsit conform selectorului, vor fi folosite următoarele metode:

- `wrap()`
- `wrapAll()`
- `wrapInner()`

Pentru a înlocui fiecare element găsit cu alte elemente sau cu text, se vor folosi următoarele metode:

- `html()`
- `text()`
- `replaceAll()`
- `replaceWith()`

Pentru a elimina elementeleconform criteriilor de selecție, se va folosi:

- empty()

Pentru a elimina fiecare element găsit, dar și descendenții acestora, dar fără a le șterge, se vor folosi metodele:

- `remove()`
- `detach()`

Să le luăm pe rând.

### 4.1 Inserarea și poziționarea elementelor în DOM

#### 4.1.1 Metodele `append()` și `appendTo()`

Metoda `appendTo()` atașează elementul specificat la punctul țintit prin specificator.

```javascript
$('ul ul:first').append('<li> Voi fi ultimul element');
```

Folosirea acestei metode permite chaining-ul.

Metoda `appendTo()` permite specificarea punctului în care se face atașarea noului element.

```javascript
$('<li>Un element nou adăugat</li>').appendTo($('ul ul:first'));
```

În cazul metodei `appendTo()` vom avea fixată legătura `this` la elementul vizat, fiind subiectul pe care se va aplica metoda. Acest lucru nu permite chaining-ul.

Pentru a beneficia de chaining, se va folosi operațiunea inversă prin folosirea metodei `append()`.

```javascript
$('ul ul:first').append('<li>Un element nou adăugat</li>');
```

Acest mod de a gândi inserția în funcție de necesitatea de a face chaining sau nu, se numește *inverted insertion methods*.

#### 4.1.3 Metoda `prepend()`

Această metodă împinge elementul chiar deasupra elementului țintit. Primește și o funcție drept argument.

```javascript
$('ul ul:first').prepend('<li> Voi fi primul element');
```

#### 4.1.4 Metoda `prependTo()`

Similar metodei `appendTo()`, avem `prependTo()`, care atașează deasupra elementului specificat. Primește și o funcție drept argument.

```javascript
$('<li>Eu voi ajunge primul</li>').prependTo('ul ul:first');
```

#### 4.1.5 Metoda `after()`

Adaugă un element sibling după cel selectat. Primește și o funcție drept argument.

#### 4.1.6 Metodele `before()` și `insertBefore()`

Metoda `before()` adaugă un element sibling înaintea celui selectat.

Metoda poate primi drept argument o funcție în loc de un selector.

```javascript
$('.carte').before(function () {
  return '<p>Urmează o carte</p>';
});
```

JQuery chiar permite introducerea unui element care poate fi țintit cu un selector.

```javascript
$('#insertie').before($('#elementExistent'));
```

Ceea ce se va petrece este o mutare a elementului existent în poziția în care a fost menționată ca punct de inserție.

Abia în cazul în care muți mai multe elemente, acele elemente vor fi copiate în noua poziție.
Pe scurt, când lucrezi cu un singur element, acesta va fi mutat. Când lucrezi cu mai multe, vor fi copiate.

Metoda `insertBefore()` primește drept argument selectorul la care se va face inserarea fragmentului dorit. Ceea ce se întâmplă este că legătura `this` se va face automat la elementul țintă.

```javascript
$('<p>Ceva</p>').insertBefore('#ancora');
```

### 4.1.7 Metoda `wrap()`

Acestă metodă permite specificarea elementului care va `îmbrăca` un anumit fragment HTML.

```javascript
var fragment = $('<p>Ceva</p>');
$('#ancora').appendTo('fragment').wrap('<div id="pachet">');
```

### 4.2 Copierea și înlocuirea elementelor

#### 4.2.1 Motoda `clone()`

Această metodă ia elementele referite de selector pentru a le putea copia ulterior.

```javascript
$('article.sectiune p:eq(0)').clone();
```

Să presupunem că dorim copierea primului paragraf dintr-un set de elemente care au clasa `sectiune` a unui element `article`. Pentru a copia elementul, va trebui făcut un chaining cu o metodă de inserare.

```javascript
$('article.sectiune p:eq(0)').clone().insertBefore('#oAncora');
```

Metoda `clone()` din oficiu nu copiază și evenimentele atașate unui element sau pe unul din descendenți. Totuși acest lucru este posibil, dacă metodei îi este pasat un parametru Boolean cu valoarea `true`.

#### 4.2.2 Metoda `replaceWith()`

Această metodă permite înlocuirea unui element cu un altul specificat.

```javascript
$('li').replaceWith('<li>Ceva nou</li>');
//sau elemente de aceeași clasă
$('.box')
```

Metoda permite pasarea unei funcții.

```javascript
$('li').replaceWith(function () {
  // poți returna un șir sau un element
  return '<li>Elemente care sunt noi</li>';
});
```

Putem înlocui cu element care există deja.

```javascript
$('li').replaceWith(function () {
  // poți returna un șir sau un element
  var primulElement = $('li:first');
  $('p').replaceWith(primulElement);
});
```

#### 4.2.3 Metoda `replaceAll()`

Este o metodă alternativă la `replaceWith()`.

```javascript
$('<p>Acesta este paragraful cu care voi înlocui</p>').replaceAll('.clasaSelectată');
```

#### 4.2.4 Metoda `remove()`

Metoda elimină elemente din DOM.

```javascript
$('li').remove();
```

Combinând mai multe metode existente în JQuery, se pot constitui adevărate sintaxe de selectivitate precisă privind elementele vizate a fi eliminate.

```javascript
$('form').children().not('input:text, textarea, br).remove();
```

#### 4.2.5 Metoda `detach()`

Această metodă permite *tăierea* unor elemente din DOM pentru a putea fi reatașate ceva mai târziu în altă zonă a DOM-ului.

```javascript
var detasate = $('li').detach();
$('#insertie').append(detasate);
```

Spre deosebire de metoda `remove()`, această metodă va ține minte și evenimentele atașate la elementele care sunt detașate.

### 4.3 Golirea conținutului

#### 4.3.1 Metoda `empty()`

Această metodă va goli de conținut un element fără să-l elimine. Toți copiii elementului selectat vor fi eliminați.

```javascript
$('#unElemP').empty();
```

### 4.4. Manipularea atributelor și proprietăților

#### 4.4.1 Metoda `attr()`

Cu ajutorul acestei metode poți accesa atributele unui element.

```javascript
var elementA = $('link-special');
console.log(elementA.attr('href')); // obții valoarea href a proprietății
```

Menționarea unui al doilea argument de tip șir, se va solda cu înlocuirea valorii atributului cu cea nouă.

#### 4.4.2 Metoda `prop()`

Această metodă permite accesul rapid la proprietățile unui element așa cum este, de exemplu, `checked` al unui element checkbox.

```javascript
var radioButton = $("input[type=radio]:first");
console.log(radioButton.prop("checked"));  // false, dacă nu este bifat
console.log(radioButton.attr("checked"));  // undefined dacă nu e bifat sau "checked"
```

În funcție de starea în care este elementul checked, metoda JQuery va returna `true` sau `false`.

### 4.5 Obținerea valorilor

în cazul în care ai nevoie de valorile elementelor, JQuery pune la dispoziție câteva metode dedicate.

#### 4.5.1 Metoda `val()`

Cu ajutorul acestei metode se poate obține valoarea unui element DOM.

```javascript
var email = $("input[type=email]").val();
var number = $("input[type=range]").val();
```

Aceeași metodă poate fi folosită pentru a seta o valoare, dacă această valoare este pasată ca argument.

```javascript
$("input[type=text]").val("Bică Simigerul");
$("input[type=range]").val(3);
```

#### 4.5.2 Metoda `text()`

Această metodă extrage textul pur dintr-un element. Toate tagurile vor fi escaped și vor fi tratate precum caracterele simple. Pentru a extrage întregul conținut HTML, se va folosi metoda `html()`.

```javascript
$('p:first').text();
```

Aceeași metodă poate fi folosită pentru a introduce text într-un element selectat dacă acesta este pasat drept prim argument metodei.

```javascript
$('p:first').text('Am schimbat conținutul elementului');
```

Metoda acceptă ca argument și o funcție cu rol de callback. Valoarea returnată din callback va fi folosită pentru a modifica conținutul text al elementului vizat.

```javascript
$('#ancora').text((index, text) => {
    // modfică cumva textul
    return text;
});
```

Argumentul `index` este poziția elementului pe care se va face modificarea textului, dacă acel element face parte dintr-un set adus prin selector. Cel de-al doilea argument `text` este textul existent anterior, care va fi supus modificării în callback. Să presupunem că avem trei elemente într-o listă neordonată.

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

Pentru a introduce text în fiecare dintre elementele `li`, putem aplica metoda pasându-i un callback.

```javascript
$( "ul li" ).text(function( index ) {
  return "Numărul elementului este " + ( index + 1 );
});
```

Exemplul va produce următoarea structură HTML.

```javascript
<ul>
  <li>Numărul elementului este 1</li>
  <li>Numărul elementului este 2</li>
  <li>Numărul elementului este 3</li>
</ul>
```

Metoda `text()` nu poate fi folosită pentru a seta valori text pe elemente `input`.

#### 4.5.3 Metoda `html()`

Această metodă extrage fragmentul de cod HTML conținut de selector.

```javascript
$('#unDiv').html();
```

Metoda va genera un fragment de text, care reprezintă codul HTML din elemntul selectat. Aceeași metodă poate fi folosită pentru a introduce cod HTML într-un element selectat dacă acesta este pasat drept prim argument metodei.

```javascript
$('#unDiv').html('<p>Acesta este un demo</p>');
```

Acest mod de a introduce cod HTML are problema că șterge ceea ce există deja în element.

Pentru a adăuga cod HTML la preexistent, se va selecta și ceea ce există.

```javascript
var divUl = $('#unDiv');
divUl.html(divUl.html() + '<p>Acesta este un demo</p>');
```

Se poate pasa și o funcție care să facă prelucrări asupra valorilor care vor fi pasate, cu mențiunea că aceasta trebuie să returneze valoarea de cod care trebuie inserată în selector.

În cazul în care metoda se află într-un lanț de transformări, trebuie returnat rezultatul pentru a putea intra ca input în următoarea metodă din lanț.

```javascript
$('#element').clone().addClass('fain').find('span.roz').html('$ellip;').end().prependTo($('#element').parent().css('color','green'));
```



## 5. Referința către obiectul context - `this`

Legătura `this` indică o referință catre un element DOM, care a declanșat un eveniment. Simpla operațiune `$(this)` va transforma un element DOM într-un obiect JQuery pe care putem aplica metode specifice.

```javascript
// un idiom util
var element = $(this);
```

Pentru a vedea cum realizează legătura `this`, vom realiza o mică galerie de imagine dinamică.

```html
    <div class="gallery">
      <img src="images/prima.jpg" alt="">
    </div>
```

Codul pentru dinamizarea galeriei

```javascript
  // selectează prima imagine pentru a stabili o primă referință
  var primaReferinta = $(".gallery").find("img").first();

  // inițializarea unui array cu linkurile care vor fi înlocuite repetitiv
  var imagini = [
    "images/aDoua.jpg",
    "images/aTreia.jpg",
    "images/aPatra.jpg"
  ];

  // constituirea unei variabile care să reprezinte indexul
  var i = 0;
  // setarea unui interval care să schimbe imaginea la 2 secunde
  setInterval(function() {
    // avem un interval de lucru cu trei valori, adică valoarea length a array-ului
    i = (i + 1) % imagini.length;  // i = 1, 2, 0, 1, 2, 0, ...

    // Trebuie schimbat atributul src al imaginii
    primaReferinta.fadeOut(function() {
      // în acest callback, "this" se va referi la primaReferinta
      $(this).attr("src", imagini[i]);
      $(this).fadeIn();
    });

    // verifica calea setată
    console.log(primaReferinta.attr("src"));
  }, 2000);
```

## 6. Manipularea valorilor CSS

JQuery pune la dispoziție metoda `css()` pentru a face modificări asupra proprietăților css ale unui element.

```javascript
// <img id="ima" src="img/prima.jpg" width="20px">
$('#ima').css('height', '30px');
// sau adăugarea valorii la cea preexistentă
$('#ima').css('height', '+=20px');
```

Aceeași metodă se poate folosi pentru extragerea valorilor proprietăților CSS.

```javascript
$('#ima').css('height'); // 30px
// pentru a obține valoarea curată
$('#ima').height(); // 30
```

Se observă faptul că JQuery oferă metode corespondente proprietăților pentru a extrage strict valoarea.

Pentru a obține un obiect cu proprietăți CSS ale unui element, metoda `css()` acceptă și un array al celor dorite pentru un anumit selector.

```javascript
$('p').css([
  'font-size',
  'line-height'
]); // Object { "font-size": "16px", "line-height": "19px" }
```

De reținut este faptul că metoda are grijă de prefixele de vendor.

## 7. Manipularea claselor

Pentru a manipula clasele unui element, se va folosi metoda `addClass()`.

```javascript
$('a').addClass('fancy-link'); // adăugarea unei clase
$('p;first').addclass('large emphasize');
$('li li').addClass(function(index){
  $(this).addClass('item-' + index); // this este lista 'li li'
})
```

Metoda `addClass()` permite și înlocuirea unei clase prin pasarea clasei curente funcției cu rol de callback.

```javascript
$('div').addClass(function(index, currentClass){
  if(currentClass === 'ceva'){
    return 'altceva';
  }
});
```

Opozabil metodei `addClass()` avem metoda `removeClass()`.

```javascript
$('#careva').removeClass('aceasta');
```

Prin înlănțuirea cu `addClass()`, se poate face înlocuirea unei clase cu alta.

```javascript
$('.aceea').removeClass('aceea').addClass('asta');
```

## 8. Stocarea și utilizarea datelor

### 8.1 Metoda `data()`

Aceast atribut poate fi asociat elementelor DOM. Datele pe care le poate oferi un element selectat sunt accesibile ca perechi cheie - valoare.

Regula este să aplici metoda `data()` pe selector, pasându-i drept prim argument numele cheii, iar al doilea parametru, însăși valoarea: `$('#unDiv').data('oProp', 'val')`.

Pentru a folosi datele, le vei accesa cu `$('#unDiv').data('oProp')`. Pentru a obține toate datele, nu trebuie pasat niciun parametru metodei `$('#unDiv').data()`.

```javascript
  // selectează elementul care găzduiește galeria
  var gallery = $(".gallery");

  // inițializarea unui array cu linkurile care vor fi înlocuite repetitiv
  var imagini = [
    "images/aDoua.jpg",
    "images/aTreia.jpg",
    "images/aPatra.jpg"
  ];

  gallery.data('imaginiDisponibile', imagini);
  // pentru a vedea ce valori sunt disponibile
  console.log(gallery.data('imaginiDisponibile')); // afișează un array cu valorile disponibile
```

### 8.2  Ștergerea datelor cu metoda `removeData()`

Pentru a elimina toate datele, se va apela la metoda `$('#unDiv').removeData()`. Dacă dorești eliminarea unei anumite proprietăți, vom pasa drept argument numele proprietății `$('#unDiv').removeData('oProp')`.

### 8.3 Utilizarea proprietății `data-*`

Dacă unui element DOM îi asociezi un atribut `data-*`, de exemplu `<p id="primul" data-primele="Ceva date utile">Acesta este un exemplu</p>`, poți să obții valoarea din acel atribut folosind metoda `data()` căreia îi pasezi ceea ce este după `data-`: `$('#primul').data('primele')`.

## 9. Tratarea evenimentelor

Mecanismul de gestionare a evenimentelor oferit de JQuery este un nivel așezat pe cel pe care browserele îl oferă. Acest nivel permite o manipulare a evenimentelor cu anumite avantaje. De exemplu, poți trimite date în obiectul eveniment sau poți executa funcțiile atașate evenimentelor, fără ca interacțiunea cu utilizatorul să fi avut loc.

În momentul în care apare un eveniment, este executată funcția cu rol de callback în interiorul căreia valoarea `this` este elementul DOM, care a inițiat evenimentul. JQuery oferă o metode care să simplifice setarea evenimentelor așa cum sunt:

- `.click()`
- `.focus()`
- `.blur()`
- `.change()`

Aceste metode simple sunt prescurtări ale metodei `.on('numeEveniment', functie)`.

### 9.1. Evenimente de mouse

Rutina lucrului cu evenimentele este aceea de a pasa metodei specializate o funcție cu rol de callback, care primește drept parametru obiectul eveniment.

#### 9.1.2. Metoda `click()`

Vom explora mai întâi cele mai cunoscute evenimente care apar. Cele generate în urma unui *click*.

```javascript
// <button id="btn-prim">Apasă-mă!</button>
$(function(){
  $('#btn-prim').click(function(event){
    console.log('Ai apăsat!');
  });
});
```

Pentru a referi obiectul DOM (selectorul) asupra căruia s-a acționat cu un click, vom folosi `$(this)`.

```javascript
// <button id="btn-prim">Apasă-mă!</button>
$(function(){
  $('#btn-prim').click(function(event){
    $(this).fadeTo(500, 0.5);
  });
});
```

Dacă dorești să se declanșeze evenimentul click ca și cum elementul ar fi fost acționat, se va apela direct click:

```javascript
// <button id="btn-prim">Apasă-mă!</button>
$(function(){
  $('#btn-prim').click(function(event){
    $(this).fadeTo(500, 0.5);
  });
  $('#btn-prim').click();
});
```

#### 9.1.3 Metoda `hover()`

Este metoda care va fi folosită pentru a trata evenimentele de hover.

```javascript
// <button id="btn-prim">Treci peste mine</button>
$(function(){
  $('#btn-prim').hover(function(event){
    $(this).text('Sunt dedesubt');
  });
});
```

În cazul lui *hover*, vom avea de-a face cu două evenimente. Unul care se declanșează la momentul în care mouse-ul *intră* pe element și al doilea pentru momentul în care mouse-ul *iese* de pe element. Pentru tratarea separată a celor două evenimente, avem metode specializate.

#### 9.1.4 Metodele `mouseenter()` și `mouseleave()`

```javascript
// <button id="btn-prim">Treci peste mine</button>
$(function(){
  var butonul = $('#btn-prim');
  // când intri, scade opacitatea
  butonul.mouseenter(function(event){
    $(this).stop().fadeTo(500, 0.8);
  });
  // când ieși, adu opacitatea la valoarea normală
  butonul.mouseleave(function(){
    $(this).stop().fadeTo(500, 1);
  });
});
```

Dacă lași tratarea evenimentelor fără metoda `stop()`, în cazul în care treci de câteva ori repede cu mouse-ul peste element, evenimentele vor continua să se declanșeze respectând timpul specificat în `fadeTo` până când nu mai există niciunul chiar dacă mișcarea mouse-ului s-a oprit demult.

Pentru a preveni un astfel de comportament, se folosește metoda `stop()`.

Alternativ acestor două metode, se poate folosi metoda `hover()` căreia îi pasezi două obiecte ce reprezintă ceea ce se petrece la intrarea pe element și ceea ce se petrece la ieșire.

```javascript
// <button id="btn-prim">Treci peste mine</button>
$(function(){
  $('#btn-prim').hover(function laIntrare (event) {
    $(this).stop().fadeTo(500, 0.8);
  }, function laIesire () {
    $(this).stop().fadeTo(500, 1);
  });
});
```

### 9.2 Atașarea funcțiilor handler cu metoda `on()`

Această metodă setează *event listeners* doar pentru elementele care există deja la momentul în care această atribuire se face.

În cazul în care dorești să atașezi aceeași funcție de răspuns (*handler*) mai multor evenimente, acestea pot fi trecute într-o înșiruire separată de spații ca prim parametru al funcției `on()`.

```javascript
$(function () {
  $('html').on('click keydown', function () {
    console.log('ai dat click sau ai apăsat vreo tastă');
  });
});
```

Dacă se vor crea elemente similare după atribuirea listener-ului, acestea nu li se va asocia evenimentul.

```javascript
$( document ).ready(function(){

    // Setează toate butoanele care au clasa `alert` care există deja în DOM
    $( "button.alert" ).on( "click", function() {
        console.log( "A fost apăsat butonul" );
    });

	// creezi un alt buton cu aceeași clasă pe care îl adaugi în DOM
    // acesta nu va avea un eveniment setat
    $( "<button class='alert'>Alertă!</button>" ).appendTo( document.body );
});
```

Pentru lizibilitate și modularitate, scoate funcțiile care gestionează evenimentul în afara metodei `on()`.

```javascript
function unMesajpentruTine () {
  console.log('ai dat click sau ai apăsat vreo tastă');
};
$(function () {
  $('html').on('click keydown', unMesajPentruTine);
});
```

În funcția setată ca event handler ai acces la mai multe proprietăți ale obiectului eveniment, care își pot dovedi utilitatea în funcție de caz:

- `pageX` și `pageY`, fiind poziția mouse-ului la momentul în care a apărut evenimentul;
- `type`, fiind tipul evenimentului - "click", de exemplu;
- `which`, care indică butonul sau tasta care a fost apăsată ceea ce a atras declanșarea evenimentului;
- `data`, fiind datele care au fost pasate la momentul în care s-a făcut atribuirea (*bounding-ul*) funcției care are rol de a răspunde evenimentului.
- `target`, fiind elementul care a declanșat evenimentul;
- `namespace`-ul care a fost specificat atunci când evenimentul a fost declanșat;
- `timestamp`, fiind marca de timp la care a apărut evenimentul;
- `preventDefault()`, împiedică reflow-ul paginii;
- `stopPropagation()` împiedică bubbling-ul.
- `this` este elementul DOM căruia i-a fost atribuită funcția handler.

Legat de `this`, este util să știi că un simplu `$(this)` va transforma un element DOM într-un obiect JQuery pe care putem aplica metode specifice.

#### 9.2.1. Schimbarea unei imagini la click

```javascript
  // selectează prima imagine pentru a stabili o primă referință
  var refGall = $(".gallery");

  // inițializarea unui array cu linkurile care vor fi înlocuite repetitiv
  var imagini = [
    "images/aDoua.jpg",
    "images/aTreia.jpg",
    "images/aPatra.jpg"
  ];

  var i = 0; // fixează indexul
  // fixează imaginea existentă și la click pe ea
  refGall.find('img').on('click', function () {
    i = (i + 1) % imagini.length; // plaja este 0, 1, 2
    // la click elimină elementul curent și la încheiere execută callback-ul
    $(this).fadeOut(function () {
      // schimbă valoarea src-ului cu, calea din array-ul imagini de la indexul specificat
      $(this).attr('src', imagini[i]).fadeIn();
    });
  });
```

### 9.3 Eliminarea evenimentului cu metoda `off()`

Pentru eliminarea unui eveniment de pe un element, se va pasa metodei `off()` numele tipului de eveniment.

```javascript
$( "p" ).off( "click" ); // șterge toate evenimentele asociate lui click
```

În cazul în care elementul are atașată o funcție handler cu nume, poți indica ca doar acel handler să fie scos, pasând numele acesteia ca parametru secund funcției.

```javascript
var una = function() { console.log( "una" ); };
var alta = function() { console.log( "alta" ); };

$( "p" ).on( "click", una ).on( "click", alta );
$( "p" ).off( "click", alta ); // va rămâne atașată funcția `una`
```

### 9.4 Rularea o singură dată - metoda `one()`

Există cazuri în care un anumit eveniment să necesite rularea o singură dată.

```javascript
$( "p" ).one( "click", primulClick );

function primulClick() {
    console.log( "Ai apăsat pentru prima dată butonul" );

    // Dacă e nevoie să mai fie apăsat în continuare, atașează un alt handler
    // dacă dorești rularea o singură dată, nu reatașa
    $( this ).click( function() { console.log( "Ai mai apăsat asta o dată" ); } );
}
```

Funcția va fi executată totuși pentru fiecare paragraf din text. Nu va fi ștearsă de pe toae evenimentele.

Metoda poate accepta mai multe tipuri de evenimente.

```javascript
$( "input[id]" ).one( "focus mouseover keydown", evenimentPrim);

function evenimentPrim( eventObject ) {
    console.log( "A apărut un eveniment " + eventObject.type + " care are id-ul " + this.id );
}
```

Setarea mai multor evenimente cu mai multe handlere.

```javascript
$( "div" ).on({
    mouseenter: function() {
        console.log( "hovered pe un div" );
    },
    mouseleave: function() {
        console.log( "mouse părăsește div-ul" );
    },
    click: function() {
        console.log( "a apărut clic pe div" );
    }
});
```

### 9.5. Delegated events

În momentul în care ai nevoie să atașezi un eveniment unui element care a fost adăugat în DOM după ce pagina a fost încărcată, vei avea nevoie să delegi evenimentul către un părinte al potențialului element viitor adăugat.

*Event delegation* se referă la faptul că este folosit *event propagation* (*bubbling*) pentru a gestiona evenimente din structura DOM-ului mai sus de poziția celui care a declanșat evenimentul. Ceea ce se petrece este o *delegare* a evenimentului către elementele părinte. Cu alte cuvinte, ori de câte ori un copil va apărea, va fi datoria părintelui să răspundă la evenimentul pe care copilul ar trebui să răspundă. Acest lucru permite atașarea de elemente în viitor care vor putea răspunde la eveniment.

```javascript
$(document).ready(function () {
   $('#btnAdd').on('click', function(){
    $('<div>Un div dinamic adăugat</div><br/>').appendTo('body');
  });
  $(document).on("click","div", function(){
    console.log("Am fost apăsat.");
  });
});
```

Un lucru foarte important de precizat este că pe măsură ce elementul părinte este mai departe de locul viitorului element, performanțele vor scădea, ceea ce face pe unii programatori să conteste folosirea evenimentelor delegat. Ca regulă de aur, atașează un eveniment delegat cât mai aproape de viitorul element.

Este permisă atașarea unui singur event listener pentru elemente care există în momentul prezent sau în viitor.

```javascript
$('#continut').on('click', 'p', function () {
  $(this).slideUp(); // this se va referi in acest caz la p, nu la #continut
});
```

Pentru a rezolva, vom pasa ca al doilea parametru, elementele sau elementul dinamic, pentru care evenimentele se vor aplica. În exemplul de mai sus, pentru toate elementele `p`, se va aplica evenimentul pasat drept al treilea parametru.

În acest caz, referința `this` se va face la elementul pasat ca al doilea parametru, nu la selector.

Poți specifica și mai detaliat atributele elementului care va fi atins de eveniment, dacă acest lucru este necesar.

```javascript
// Ataașarea unui delegated event la un element cu un anume atribut
$( "#lista" ).on( "click", "a", function( event ) {
    var elementulArumentDoi = $( this );
    if ( elementulArumentDoi.is( "[href^='http']" ) ) {
        elementulArumentDoi.attr( "target", "_blank" );
    }
});
```

Pentru simplitate, specificitatea selectorului poate fi menționată direct în al doilea parametru.

```javascript
$( "#lista" ).on( "click", "a[href^='http']", function( event ) {
    $( this ).attr( "target", "_blank" );
});
```

### 9.6. Trimitere unor date suplimentare unui eveniment

În funcție de caz, este posibilă trimiterea unor date suplimentare obiectului eveniment către funcția de prelucrare asociată (*handler*).

```javascript
// Setarea evenimentului folosind metoda `.on()`, adăugând date
$( "input" ).on(
    "change",
    { ceva: "informatii" }, // Asociază date la momentul de event binding
    function( evt ) {
        console.log("S-a modificat valoarea unui input ", evt.data.ceva);
    }
);
```

Atunci când este necesară trimiterea de date suplimentarea în cazul unui eveniment, acestea vor fi introduse într-un obiect ca prim parametru al metodei `click()`, de exemplu.

```javascript
$('#butonul').click({
  prima: 'ceva'
}, function (event) {
  oFunctieDePrelucrare(event.data);
});
// funcția handler
function oFunctieDePrelucrare (datele) {
  let prima = datele.prima; // "ceva"
}
```

Datele pasate evenimentului vor fi disponibile funcțiilor de prelucrare ca proprietate distinctă a obiectului `event`. Datele sunt disponibile din `event.data`.

#### 9.6.1. Crearea unei galerii cu preview lightbox

```javascript
$(function () {

  // Constituie un array cu toate imaginile din selector.
  var galleryItems = $(".gallery").find("img");

  // dacă nu este setat in CSS, poți încerca setarea din JQuery
  galleryItems.css("width", "30%").css("opacity", "0.7");

  // la hovering pe imagine, adu opacitatea la maxim
  galleryItems.mouseenter(function() {
    $(this).stop().fadeTo(500, 1);
  });
  // la ieșirea de pe element imagine, modifică transparența
  galleryItems.mouseleave(function() {
    $(this).stop().fadeTo(500, 0.7);
  });

  // fă o previzualizare în lightbox atunci când dai click.
  galleryItems.click(function() {
    //citeste src-ul imaginii pe care s-a apăsat
    var source = $(this).attr("src");

    // Generează un nou tag <img> care să fie adăugat în lightbox.
    var newImage = $("<img>").attr("src", source).css("width", "100%");

    // golește de conținut lightbox-ul si fa preview.
    $(".lightbox").empty().append(newImage).fadeIn(1000);
  });

  // atunci cand dai click oriunde, ieși din lightbox.
  $(".lightbox").click(function() {
    $(this).stop().fadeOut();
  });

});
```

### 9.7. Evenimente de tastatură

Evenimentele `keyup` și `keydown`. Evenimentul `keydown` returnează tasta care a fost apăsată.

```javascript
$('html').keydown(function (event) {
  console.log(event.which);
});
```

Obiectul `which` este unul pe care JQuery îl adaugă. Avantajul este că JQuery înlătură toate inconsistențele dintre browsere.

### 9.8. Formulare

#### 9.8.1 Evenimentul `focus`

```javascript
var campuriForm = $('input:text, input:password, textarea');
campuriForm.focus(function () {
  // atunci când unul dintre câmpuri primește focus
  $(this).css('box-shadow', '0 0 4px #655');
});
campuriForm.blur(function () {
  // când câmpul  pierde focus-ul
  $(this).css('box-shadow', 'none');
});
```

#### 9.8.2. Evenimentul `blur`

```javascript
var campuriForm = $('input:text, input:password, textarea');
campuriForm.focus(function () {
  // atunci când unul dintre câmpuri primește focus
  $(this).css('box-shadow', '0 0 4px #655');
});
campuriForm.blur(function () {
  // când câmpul  pierde focus-ul
  $(this).css('box-shadow', 'none');
});
// poți iniția verificări sau transformări per câmp
$('#email').blur(function () {
  var text = $(this).val();
  if (text.length < 3) {
    $(this).css('box-shadow', '0 0 4px #811');
  } else {
    $(this).css('box-shadow', '0 0 4px #181');
  }
});
```

#### 9.8.3. Evenimentul `change`

Este evenimentul folosit în cazul checkbox-urilor, butonanelor radio și a select-urilor. Poți atașa evenimente care să trateze cazul în care utilizatorul a uitat să bifeze un checkbox sau un radio.

```javascript
$(function () {
  $('#checkbox).change(function () {
    var isChecked = $(this).is(':checked'); // poți folosi și prop('checked')
    if (ischecked) {
      $(this).add('label[for='cb']').css('box-shadow', '0 0 4px #181');
    } else {
      $(this).add('label[for='cb']').css('box-shadow', '0 0 4px #811');
    }
  });
  $('#selection').change(function () {
    var selectedOption = $(this).find(':selected').text(); // obții textul unei singure selecții
  });
});
```

#### 9.8.4. Evenimentul `submit()`

```javascript
$('#form').submit(function () {
  var nume = $('#nume').val();
  var email = $('#email').val();
  var checked = $('#checkbox').is(':checked');
});
```

### 9.9 Executarea funcție handler cu metoda `trigger()`

JQuery permite executarea funcției cu rol de `event handler` fără să necesite intervenția utilizatorului. Acest lucru este posibil pentru că JQuery ține o referință către funcția handler la momentul când aceasta a fost legată de un anume eveniment.

Această metodă își dovedește utilitatea maximă în cazul definirii de evenimente custom.

Opțional, metodei `trigger()` i se poate pasa un al doilea parametru, care să fie un array de valori. Acest array de valori, vor fi pasate funcției handler ca argumente, imediat după ce a fost pasat obiectul event.

### 9.10 Evenimente custom

Ceea ce permit aceste evenimente particularizate, este o refocalizare de la evenimentul care a declanșate execuția unui listener, pe elementele care sunt afectate de eveniment.

```html
<div class="camera" id="sufragerie">
    <div class="bec aprins"></div>
    <div class="ruptor"></div>
    <div class="ruptor"></div>
    <div class="intrerupator"></div>
</div>
```

Ceea ce dorim este ca acționând asupra elementelor care au clasa `ruptor` și `intrerupator` să modifici clasa `aprins` în `stins`. O soluție fără evenimente personalizate ar fi.

```javascript
$(".ruptor, .intrerupator").click(function () {
    var bec = $(this).closest('.camera').find('.bec');
    if (bec.is('.aprins')) {
        bec.removeClass('.aprins').addClass('.stins');
    } else {
        bec.removeClass('stins').addClass('aprins');
    }
});
```

Folosind evenimente personalizate, se poate construi următoarea logică.

```javascript
// pune un eveniment custom chiar pe elementul care își va schimba starea
$('.bec').on('bec:toggle', function (evt) {
    var bec = $(this);
    if ( bec.is('.aprins') ){
        bec.removeClass('.aprins').addClass('.stins');
    } else {
        bec.removeClass('.stins').addClass('.aprins');
    }
});

$('.ruptor, .intrerupator').click(function () {
    var camera = $(this).closest('.camera');
    camera.find('.bec').trigger('bec:toggle');
});
```

Ceea ce am reușit este să mutăm acțiunea de pe elementele cu clasele care aveau potențialul de a modifica starea, chiar pe elementul care trebuie modificat. Numele evenomentului particular, conform documentației, poate fi orice string, dar trebuie avut în vedere să nu fie identic cu unul deja existent pentru care browserul are un anumit comportament. Pentru simplitate și siguranță, s-a ales formula `bec:` pentru denumire.

Să extindem comportamentul.

```html
<div class="camera" id="sufragerie">
    <div class="bec aprins"></div>
    <div class="ruptor"></div>
    <div class="ruptor"></div>
    <div class="intrerupator"></div>
</div>
<div class="camera" id="dormitor">
    <div class="bec aprins"></div>
    <div class="ruptor"></div>
    <div class="ruptor"></div>
    <div class="intrerupator"></div>
</div>
<div id="heblu"></div>
```

În cazul acesta extins, divul care are clasa `heblu` ar trebui să pună toate becurile pe clasa `stins`.

```javascript
$('.bec')
    .on('bec:toggle', function () {
        var bec = $(this);
        if ( bec.is('.aprins') ){
            bec.trigger('bec:stins'); // adaugă un nou custom event
        } else {
            bec.trigger('bec:aprins');// adaugă un nou custom event
        }
    })
    .on('bec:aprins', function (event) {
    	$(this).removeClass('stins').addClass('aprins');
	})
	.on('bec:stins', function (event) {
    	$(this).removeClass('aprins').addClass('stins');
	});

// acționarea individuală în funcție de acționarea div-urilor selectivă
$('.ruptor, .intreruptor').click(function () {
    var camera = $(this);
    camera.find('.bec').trigger('bec:toggle')
});

// acționarea div-ului heblu
$('#heblu').click(function () {
    var becuri = $('.bec');

    // verifică dacă vreun bec este aprins
    if (becuri.id('.aprins')) {
        becuri.trigger('bec:stins');
    } else {
        becuri.trigger('bec:aprins');
    }
});
```

Un exemplu de utilizare a metodei `trigger()`, dar care primește un array pe poziția celui de-al doilea parametru.

```javascript
$( document ).on( "evenimentParticularizat", {
    ceva: "date"
}, function( event, arg1, arg2 ) {
    console.log( event.data.ceva ); // "date"
    console.log( arg1 );            // "unu"
    console.log( arg2 );            // "doi"
});

$( document ).trigger( "myCustomEvent", [ "unu", "doi" ] );
```

Ca încheiere, evenimentele custom permit un transfer al atenției de pe elementul care produce schimbarea, pe elementul care suferă schimbarea. Astfel, vei putea acționa acele elemente individual sau pe toate odată. Din momentul în care comportamentul a fost descris pentru un anumit element prin intermediul unui custom event, este ușor să triggeruiești acele comportamente descrise de oriunde din cod.

## 10. Încărcarea resurselor de web

Pentru a încărca o resursă la distanță, JQuery oferă câtea metode foarte utile.

### Încărcarea de pe disk - metoda `load()`

Pentru a încărca conținutul unei resurse de pe disk, poți folosi metoda `load()`. Mai întâi trebuie selectat locul unde se va încărca resursa.

```javascript
$('#locul').load('date/date.json');
// încărcare cu verificarea existenței resursei
$('#locul').load('date/meteo.csv', function (response, status) {
  if (status == 'error') console.log('A apărut o eroare la încărcare');
  console.log(response);
})
```

### Metoda `getJSON()`

```javascript
var url = 'http://undeva.ro/meteo.json'
$.getJSON(url, {
  // opțiuni
}).done(function () {
  // prelucrează răspunsul
}).fail(function () {
  // tratează erorile
})
```

## JQUERY UI

Biblioteca de cod este împărțită în patru componente mari:

- interacțiune
- efecte
- widgets
- utilitare.
