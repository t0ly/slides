## Как програмирането на ниско ниво ни прави по-добри програмисти на високо

---------------------
Никола Димитров

<a href="mailto:nikola@dimitroff.bg"><i class="fa fa-envelope-o"></i>nikola@dimitroff.bg</a> </br>
<a href="https://github.com/nikoladimitroff"><i class="fa fa-github"></i>/nikoladimitroff</a> </br>


<a href="https://dimitroff.bg"><i class="fa fa-rss"></i> dimitroff.bg</a> / <a href="https://coherent-labs.com"> coherent-labs.com</a>


--- NEXT SLIDE ---

![Logos](slides/resources/hackconf2016-cpp-is-great/coh-logos.png)

--- NEXT SLIDE ---

![C++ as monster](slides/resources/hackconf2016-cpp-is-great/cppthulhu.jpg)

--- NEXT SLIDE ---

![The C++ scrolls](slides/resources/hackconf2016-cpp-is-great/cpp-scrolls.png)

```cpp
// ES6
[1, 2, 3].map(x => x * x);
```

```cpp
// C++
vector<int> input = {1, 2, 3};
vector<int> output;
transform(input.begin(), input.end(),
          output.begin(), output.end(),
          [](int x) { return x * x; });
```

Note: Налага ми се да пиша на C++, което в някои аспекти си е страшно.
Доста неща работят сякаш на МАГИЯ. Например познайте какво е това:
Само в C++ компилаторът ви може да ви даде такава грешка:

--- VERTICAL SLIDE ---

```cpp
#include <vector>
#include <algorithm>
int main()
{
    int a;
    vector<vector<int>> v;
    auto it = find(v.begin(), v.end(), a /* <-- */);
}
```

160 байта код =
15 786 байта грешка

> /usr/include/c++/4.6/bits/stl_algo.h:162:4: error: no match for ‘operator==’ in
> ‘__first.__gnu_cxx::__normal_iterator::operator*
> [with _Iterator = std::vector*, _Container = std::vector >, __gnu_cxx::__normal_iterator::reference = std::vector&]() == __val’
> ...

Note:
Дори съществува състезание за най-дълга грешка от най-малко написан код!
Source for the code - http://codegolf.stackexchange.com/questions/1956/generate-the-longest-error-message-in-c

--- VERTICAL SLIDE ---

![wtf](https://img.memecdn.com/confused-black-girl---confusception_gp_3489431.jpg)

И още - http://tgceec.tumblr.com/

--- VERTICAL SLIDE ---

![Defence against the dark arts](slides/resources/hackconf2016-cpp-is-great/nikola-as-snape.png)

Note: Но спокойно, аз ще ви предпазя от всичката гадория. Даже бихте
могли да ме наречете вашия учител по защита от тъмните изкуства

--- NEXT SLIDE ---

На кратко:

JS + C++ = JS++

--- NEXT SLIDE ---

Език от ниско ниво?

--- VERTICAL SLIDE ---

<ol>
<li>Машинен код</li>
<li>Асемблер</li>
<strong><em>2.5. C / C++</strong></em>
<li>Java / C# / JS</li>
<li>SQL</li>
<li>Prolog</li>
</ol>

--- NEXT SLIDE ---

![Свобода](slides/resources/hackconf2016-cpp-is-great/freedom.jpg)

Note: Какво е общото между тези езици? За какво ни е свобода?

--- NEXT SLIDE ---

* *Истинска* платформена независимост
    - <!-- .element class="fragment" data-fragment-index="0" --> Пуснете си Java-та на Xbox One плс
    - <!-- .element class="fragment" data-fragment-index="1" --> https://github.com/facebook/react-native/issues/2033

--- VERTICAL SLIDE ---

* *Бързодействие*
    - <!-- .element class="fragment" data-fragment-index="1" --> математика? (графика, ИИ, игри)
    - <!-- .element class="fragment" data-fragment-index="2" --> системи в реално време? (SpaceX, Hololens, IPhone)
    - <!-- .element class="fragment" data-fragment-index="3" --> колко пъти си заредихте батерията на телефона?

Note: Винаги има смисъл да гоните бързодействие
дотолкова, колкото клиента усеща.

Пък ако съвсем не искате да пестите ресурс на клиента,
можете да оптимизирате програмта и да копаете bitcoins през спестеното време.

--- NEXT SLIDE ---

Та какъв е смисъла?

<!-- .element class="fragment" data-fragment-index="0" --> ![Hermione](slides/resources/hackconf2016-cpp-is-great/hermione.gif)

Note: Няма да ви кажа, че C++ е най-якия език на света

--- NEXT SLIDE ---

Закон за изтичащата абстракция

--- VERTICAL SLIDE ---

![Joel Spolsky](slides/resources/hackconf2016-cpp-is-great/joel-spolsky.jpg)

http://joelonsoftware.com

--- VERTICAL SLIDE ---

```js
function appendOneAtATime(count) {
    for (let i = 0; i < count; i++) {
        document.body.innerHTML += '<div></div>';
    }
}
function appendAll(count) {
    let fragment = document.createDocumentFragment();
    for (let i = 0; i < count; i++) {
        let el = document.createElement('div');
        fragment.appendChild(el);
    }
    document.body.appendChild(fragment);
}
```

http://pastebin.com/ahRT0DgS

--- NEXT SLIDE ---

<subscript>* Внимание, не се препоръчва за хора със слаби сърца</subscript>

--- VERTICAL SLIDE ---

Дефиниция на променлива
```cpp
int x = 5;
```

Присвояване по стойност (копие)
```cpp
int y = x;
```

Псевдоними

```cpp
int& z = x;
```

--- VERTICAL SLIDE ---

```js
var x = 10;
var y = x; // Копие

var z = { prop: 10 };
var w = z; // Псевдоним
```

--- NEXT SLIDE ---

## Изключения

--- VERTICAL SLIDE ---

![Filters](slides/resources/hackconf2016-cpp-is-great/exception-map.png)

--- VERTICAL SLIDE ---

```js
function mySqrt(num) {
    if (num < 0)
        throw new Error("Argument can't be negative!");
    return Math.sqrt(num);
}
function doSomeMath() {
    var num = parseInt(prompt("Please enter a number"));
    mySqrt(num); // Къде отива кода ако входа е -5?
}
```

http://www.joelonsoftware.com/items/2003/10/13.html

--- VERTICAL SLIDE ---

### Кодове за грешки

```cpp
enum class ErrorCode {NoError, InvalidArgument};
ErrorCode MySqrt(double num, double& result)
{
    if (num < 0)
        return ErrorCode::InvalidArgument;
    result = sqrt(num);
    return ErrorCode::NoError;
}
void DoSomeMath()
{
    double result = 0;
    ErrorCode code = MySqrt(-5, result);
    if (code != ErrorCode::NoError)
        cout << "Sqrt failed! " << endl;
}
```

--- VERTICAL SLIDE ---

### Скриване на грешки

```cpp
void ShootEnemy(Player* player, Enemy* enemy)
{
    if (enemy == nullptr)
    {
        cout << "Can't shoot a nonexisting enemy" << endl;
        return;
    }
    ...
}
void OnMouseDown()
{
    Shoot(player, badGuy);
}
```

--- NEXT SLIDE ---

#### const correctness
* Изкуството да не се променяш

--- VERTICAL SLIDE ---

```cpp
// Ще преизползва file
bool EndsWith(string& str, string& suffix);
// Ще преизползва file и сме сигурни, че няма да го промени
bool EndsWith(const string& str, const string& suffix);
int main()
{
    string file = "nikola-as-snape.png";
    printf("Is this file a png? %d", EndsWith(file, ".png"));
}
```

--- VERTICAL SLIDE ---

```cpp
class Rectangle
{
private:
    int Width;
    int Height;
public:
    // Тази функция няма да промени вътрешното състояние на правоъгълника
    int GetArea() const
    {
        return Width * Height;
    }
};
```

--- NEXT SLIDE ---

### Генериране на код
* И изкуството да променяш средата

--- VERTICAL SLIDE ---

```py
[x * x for x in (1, 2, 3)] // 1, 4, 9
```

Vs.

```cpp
int main() {
    vector<int> myList = { 1, 2, 3 };
    auto transformed = PythonRange(x * x forevery x inside myList);

    for (const auto& x : transformed)
    {
        cout << x << endl;
    } // 1, 4, 9
}
```

http://pastebin.com/8JLwmbFA

--- NEXT SLIDE ---

### Data-oriented programming

--- VERTICAL SLIDE ---

* ~~Абстракция~~
* ~~Енкапсулация~~
* ~~Наследяване~~
* <!-- .element class="fragment" data-fragment-index="0" --> Данноважност

--- VERTICAL SLIDE ---

* Код < данни
* Модел в кода != модел на света

--- VERTICAL SLIDE ---

```cpp
class Chair
{
    Vector3 Position;
    Model3D ChairModel; // <--- Трябва само за рисуването
    int ComfortLevel; // <--- Трябва само за изкуствения интелект
    PhysicsModel PhModel; // <--- Трябва само за физичната симулация
};
class ArmChair : public Chair { ... }
class SwivelChair : public Chair { ... }
...
vector<Chair> chairs;
Draw(chairs);
SimulatePhysics(chairs);
ConsiderChairsForAI(chairs);
```

--- VERTICAL SLIDE ---

```cpp
class Chair { ... }
class ChairForPhysics : public Chair
{
    PhysicsModel PhModel;
};
class ChairForAI : public Chair
{
    int ComfortLevel;
};
...
```

Note: Новият въпрос - какво ни интересува, че нещото е стол?

--- VERTICAL SLIDE ---

```cpp
class PhysicsObject
{
    int Id;
    PhysicsModel Representation;
};
class ComfortableItem
{
    int Id;
    int ComfortLevel;
};
...
vector<PhysicsObject> objectsWorthSimulating;
SimulatePhysics(objectsWorthSimulating);

vector<ComfortableItem> comfortableItems;
ConsiderForAI(comfortableItems);
```

--- NEXT SLIDE ---

## Да обобщим

* <!-- .element class="fragment" data-fragment-index="0" --> C++ е императивно-функционален
* <!-- .element class="fragment" data-fragment-index="1" --> C++ е обектно ориентиран към данни
* <!-- .element class="fragment" data-fragment-index="2" --> C++ е (не)променяем.
* <!-- .element class="fragment" data-fragment-index="3" --> C++ ви бърка в мозъка

<!-- .element class="fragment" data-fragment-index="4" --> ![Cpp bf](slides/resources/hackconf2016-cpp-is-great/scumbag-cpp.png)

Note: т.е. C++ е онова гадже, което много обичате, въпреки че ви лази по нервите.

--- NEXT SLIDE ---

Slides @

https://nikoladimitroff.github.io/slides
