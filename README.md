<h1>ParkOn</h1>

<p>Проект выпускной практики на курсах Frontend разработки на портале <a href="https://geekbrains.ru">Geekbrains</a> от Mail.ru Group.</p>
<br>
<p>Проект представляет собой Progressive Web App-приложение написаннное на фреймфорке React.js
<br>
  На репозитории выложена production сборка в целях защиты интелектуальной собственности разработчиков и продуктоунера команды ParkOn.Мы планируем поддерживать и развивать проект после его выхода на рынок,а так же развивать и улучшать функционал по мере увеличения колличества пользователей.
<br><b>Development-сборка доступна только по индивидуальному запросу.</b>
  
  
 Для проверки функционала приложения необходимо запустить тестовый сервер командой <code>npm run dev</code>,предварительно запустив OpenServer+MongoDB и сборку разработчика frontend части.
 
 <br>
 Все права интелектуальной собственности на код сервера принадлежат Абзалу Танкибаеву.
 <br>
 Backend-разработчик:<a href="mailto:AbzalT@list.ru">Абзал Танкибаев</a>
 <br>
 <a href="https://github.com/AbzalT/parkon">Сборка тестового сервера</a>
 <br>
 <a href="https://hh.kz/resume/46794fc2ff060945d60039ed1f34373668386f">Резюме backend-разработчика</a>
 
 <a href="https://github.com/AbzalT">Репозиторий backend-разработчика</a>
 
 
 
 <h4>Контакты</h4>
  <br>
  Продуктоунер:<a href="mailto:marfuny95@mail.ru">Илья Литвинов</a>
  <br>
  <br>
  На данный момент приложение находится в тестовом режиме.На момент презентации продукта нами был арендован виртуальный VDS сервер на хостинге <a href="https://firstvds.ru"> firstvds.ru</a> c VNZ-виртуализацией и Ubuntu 18.4 arm64. 
  <br>
  На 17.07.2020 аренда сервера закончена.
</p>
<h2>Основные возможности приложения:</h2>
<br>


<ul>
  <li>Возможность регистрации по СМС(Временно недоступно в тестовом режиме)</li>
  <li>Возможность регистрации по почте (Требуется тестовый сервер+development-сборка)</li>
  <li>Вход по почте или номеру телефона (Требуется тестовый сервер+development-сборка)</li>
  <li>Отображение точек парковок на Яндекс.Картах</li>
  <li>Возможность построения маршрута от текущей позиции пользователя</li>
  <li>Возможность перехода на экран трансляции конкретной зоны парковки(На данный момент имеется только одна камера).</li>
  <li>Отображение колличества свободных мест(Тестовый ручной режим.Камера и сервер нейронной сети работают в связке. На 17.07.2020 камера и сервер ИНС отключены)</li>
  <li>Возможность отправки письма на email поддержки(Требуется тестовый сервер+development-сборка)</li>
  <li>Возможность сохранения домашнего адреса для последующего использования на карте(Тестовый режим)</li>
  
  
  <h3>(!) Проект выполнен по MVP</h3>
  <h5>Реализован не весь функционал приложения.Дополнительные функции и возможности такие как голосовой поиск и поиск по адресам будут реализованы нами в будущем.Улучшение стабильности и функционала так же будут внесены при следующих обновлениях.</h5>
  
  
  <h2>Структура приложения:</h2>
  
  
![Ierarchy](https://raw.githubusercontent.com/Dmitri2205/Portfolio/master/img/Ierarchy.png)


<br>
<p>Навигация между основными и дополнительными модулями осуществляется посредством изменения состояния компонента App.jsx и его ближайших дочерних компонентов(Changeauto\Changereg\MainScreen\MapModule\Stream\Training\Welcome*.jsx).


![State](https://raw.githubusercontent.com/Dmitri2205/Portfolio/master/img/AppState.png)


<br>
  Для управления глобальным состоянием приложения в зависимости от действий пользователя с компонентами нижних уровней используются колбэк функции,которые передаются от компонента-родителя в качестве props и вызываются внутри дочернего элемента с одним из аргументов для обработки состояния отображаемого экрана внутри App.jsx.Каждый компонент отрисовывается только в том случае,когда ему передан параметр который проверяется с помощью тернарного оператора и инлайн-стилей, и позволяет нам отрисовать те или иные элементы и компоненты в зависимости от условия или набора условий переданных от компонента к компоненту как вниз по иерархии,так и вверх.
  
  
  ![Select function](https://raw.githubusercontent.com/Dmitri2205/Portfolio/master/img/App.jsx.png)


Пример условия отрисовки компонента:


<code><div className="myDiv" style={{this.props.visible ? {display:'block'}:{display:'none'} }}></div></code>
<br>
Некоторые из главных экранов(далее "Компоненты")имеют дочерние компоненты,такие как: 
<br>
<br>
Changereg => EmailRegistration\PhoneRegistration
<br>
Changeauto => EmailValidation\PhoneValidation
<br>
MapModule => About\Feedback\Personal\Personalroom
<br>
<br>


Дочерние компоненты написаны на основе классов, и имеют независимую логику и разметку HTML/CSS.

Определение местоположения ползователя происходит посредством <a href="https://tech.yandex.ru/maps/jsapi/">Yandex Maps JS API</a>.
Так же исползован модуль <code>react-yandex-maps</code>




С помощью такой структуры приложения нам удалось отказаться от использования модуля react-router в продакшн сборке,а так же улучшить стабильность и быстродействие приложения.Стили и адаптив подключены к главному компоненту App.jsx.Так же по необходимости используются инлайн-стили для конкретных элементов.
<br>
Использование React-Redux не предусмотренно и не имеет смысла.Все необходимые данные хранятся в LocalStorage браузера/PWA и являются строками.
</p>



<a href="https://github.com/Dmitri2205/Portfolio/raw/master/misc/ParkOn%20-%20REST%20API.xlsx" download >пример запросов REST API написаный нашим backend-разработчиком</a>
<br>

<h4>Зависимости:</h4>


<p>Dependencies</p>
<ul>
  <li>@babel/polyfill:7.8.7</li>
  <li>axios:0.19.2</li>
  <li>jsmpeg-player:3.0.3</li>
  <li>react:16.13.1</li>
  <li>react-dom:16.13.1</li>
  <li>react-yandex-maps:4.3.0</li>
</ul>

<br>
<p>DevDependencies</p>
<ul>
  <li>@babel/core:7.9.0</li>
  <li>@babel/plugin-proposal-class-properties:7.8.3</li>
  <li>@babel/preset-env":7.9.5</li>
  <li>@babel/preset-react:7.9.4</li>
  <li>babel:6.23.0</li>
  <li>babel-loader:8.1.0</li>
  <li>css-loader:3.5.2</li>
  <li>file-loader: 6.0.0</li>
  <li>prop-types: 15.7.2</li>
  <li>style-loader:1.1.3</li>
  <li>webpack:4.42.1</li>
  <li>webpack-cli:3.3.11</li>
  <li>webpack-dev-server:3.11.0</li>
</ul>





























