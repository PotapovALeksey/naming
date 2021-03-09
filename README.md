## Хорошие практики именования переменных, методов

<ul>
<li>
<h4>1. Имена должны передавать намерения программиста и создавать понимание того что происходит в коде.
   Имя переменной должно отвечать на вопросы: что в ней хранится, для чего она существует, и где используется 
</h4>
Пример 1.1:
<pre>
function filtering(array, code) { 
   return array.filter(item => item.code === code);
}

const result = filtering(list, 4);
</pre>

Этот пример создает только еще больше вопросов
- что конкретно фильтрует метод
- зачем нужно значение 4
- что хранится в списке list

Пример 1.2:
<pre>
const ACTIVE_ACCOUNT_CODE = 4;

function filteringAccounts(accounts, code) { 
   return accounts.filter(item => item.code === code);
}

const filteredAccounts = filteringAccounts(accounts, ACTIVE_ACCOUNT_CODE);
</pre>


Этот же код является намного очевиднее и передает намерения программиста:
- есть понимаение что мы работаем с аккаунтами
- константа с кодом активного аккаунта
- метод который фильтрует аккаунты по коду
</li>


<li>
<h4>2. Избегайте дезинформации</h4>

<pre>
 Плохо:
 const accountsList = [UA12312, UA3465];  // Ожидается массив массивов
 
 Хорошо:
 const accounts = [UA12312, UA3465];
    или 
 const accountList = [UA12312, UA3465];
</pre>

</li>


<li>
<h4>3. Избыточные имена</h4>
<pre>
 Плохо
 const customerInfo;
 const accountData;
 const nameString;
</pre>
В данном примере слова: info, data не несут никакой информации, а значит избыточны
Имя не может быть числом, либо еще чем-то отличным от строки а значит приставка String избыточна
<pre>
 Хорошо
 const customer;
 const account;
 const name;
</pre>
</li>
<li>
<h4>4. Используйте выразительные и произносимые имена переменных, без сокращений и скрытого смысла</h4>
<pre>
  Плохо:
  const yyyymmdstr = moment().format('YYYY/MM/DD'); - не произносимое, при общении с другим программистом упоминать о данной перемнной будет не удобно
  const userAcc = 'UA124124'; - сокращение, при использовании в коде может быть не очевидно что там может хранится, придется идти в место объявления
  const onChange = (e) => ....; - сокращение
</pre>
<pre>
  Хорошо:
  const currentDate = moment().format('YYYY/MM/DD');
  const userAccounts = ''UA124124';
  const onChange = (event) => ....;
</pre>
</li>
<li>
<h4>5. Избегайте мысленных связей</h4>
<pre>
 Плохо:
 const locations = ['Austin', 'New York', 'San Francisco'];
 locations.forEach((l) => {
   doStuff();
   doSomeOtherStuff();
   // ...
   // ...
   // ...
   // Стойте. Еще раз, что такое `l`?  Код должен быть максимально очевидным, что бы не приходилось запоминать подозрительные переменные, явное лучше чем не явное
   dispatch(l);
 });
</pre>
<pre>
Хорошо:
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});</pre>
</li>
<li>
<h4>6. Имена методов</h4>
Имена представляют собой глаголы или глагольнный словочетания
<pre>
createTransaction
deleteTransaction
</pre>
Методы чтения/записи и предикаты(проверки) образуются из значения и префикса get, set и is
<pre>
getName
setName
isAdmin
</pre>
</li>
<li>
<h4>7. Имена булевых значений принято называть с приставкой - is, has, should </h4>
<pre>
isDisabled
hasAccount
shouldRenderRejectButton
</pre>
</li>
<li>
<h4>8. Одно имя для каждой концепции</h4>
Выберите одно слово для представления одной абстракной концепции

Например в разных моделях для загрузки данных должно использоватся одно из имен:
- load (у нас на проэкте)
- fetch
- retrieve

если в разных моделях одинаковые по смыслу методы будут иметь разные названия это создатся лишнюю путаницу
</li>
<li>
<h4>9. Содержательный контекст</h4>
Не все имена и переменные говорят сами за себя, но в контекста многий код становится более понятнее
Хороший пример именование файлов в нашем проэкте: 

    components
    ├── component-name/
        ├── component-name-child        подкомпоненты
        │    ├── ...
        │    │    └── ...
        │    └── ...
        │
        ├── component-name.styles.ts    набор стилей для компонента (required)
        ├── component-name.tsx          компонент для отображения и переиспользования (required)
        │
        ├── component-name.props.ts     интерфес компонента для наследования (optional)
        ├── component-name.selector.ts  селектор для обработки и/или управления данными в самом компоненте (optional)
        └── component-name.options.ts   наборы правил для отображения и управления компонентом (optional)

В случае переменных контекст можно добавить с помощью приставки

<pre>
 Плохо
 const sender = { ... };
 const recipient = { ... };
 const accounts = [...]; - к кому относятся эти аккаунты к sender || recipient;
    
 Хорошо
 const sender = { ... };
 const recipient = { ... };
 const senderAccounts = [...];
</pre>

</li>
<li>
<h4>10. Не нужный контекст</h4>
Если ваше имя класса/объекта говорит за себя, не повторяйте его в имени переменной.
<pre>
 Плохо
 const Car = {
   carMake: 'Honda',
   carModel: 'Accord',
   carColor: 'Blue'
 };
 </pre>

 <pre>
 Хорошо
 const Car = {
   make: 'Honda',
   model: 'Accord',
   color: 'Blue'
 };
</pre>
</li>
</ul>
