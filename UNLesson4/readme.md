####  Занятие #4 footer на место, layout, изображения и слои

# Супер- фишка шаблонизатора pug - `Layouts`  
 В папке #source создаем каталог layout, а в нем создаем файл base.pug следующего содержания:  
 ```
doctype html
html
  body
    //- подключим head
    include ../includes/head.pug
  block header
    .header
      h1 Заголовок h1
      p Добро пожаловать на мини-сайт.
      nav.navigation
        a(href="/") Главная
        a(href="about.html") О нас
        a(href="works.html") Наши работы
  block content
    .main-content

  block footer
    //- подключим footer
    include ../includes/foot.pug
 ```  
 
 Да это по сути наш файл index.pug с единственным отличием - контен обозначен блоками `block`.  
 Файл `index.pug` приводим к следующему виду:  
```
extends layout/base.pug


block content
  .main-content
    p Контент главной страницы
```  





#### Лучший(по моему мнению) способ прижать footer к низу страницы

Задаем высоту тегу html  равную 100%:

```
html {
    height: 100%;
}

```  
 Для body:  

```
body {
  display: flex;
  flex-direction: column; // главную ось располагаем вертикально, а не слева направо.
  height: 100%;
  margin: 0; // Устанавливает величину отступа от каждого края элемента
  padding: 0; // Устанавливает значение полей вокруг содержимого элемента
  overflow: hidden; //Отображается только область внутри элемента, остальное будет скрыто.
}

```  
Для класса header:  

```
.header {
    flex: 0 0 auto;
}

```  
Затем классу с контентом `main-content` передаем свойство flex,   
и говорим что элементы внутри могут расширяться(1) по высоте, но не по ширине (0):

```
.main-content {
    flex: 1 0 auto;
}
```  
```
.footer {
  flex: 0 0 auto;
  height: 65px;
  background: #337AB7 ;
  padding: 25px;
  p {
    color: #fff;
  }
}

```  


#  Изображения

Пример 1. текст поверх изображения.  
Создаем в папке #source файл works.pug, следующего содержания:  
```
extends layout/base.pug //- используя наш шаблон изменяем лишь блок 

block content
  .main-content
    .p-block
      .portfolio-item
        img(src="../img/image1.jpg")
        .portfolio-bg
          h1 Название
          h3 Описание
      .portfolio-item
        img(src="../img/image2.jpg")
        .portfolio-bg
          h1 Название
          h3 Описание
```  
works CSS:  
```
// Наши работы //
.header {}
.main-content {
  padding: 0 45px;
}
.p-block {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.portfolio-item {
  position: relative;
  display: block;
  background-size: cover;
  background-position: center;
  height: 300px;
  max-width: 100%;

}
.portfolio-bg {
  position:absolute;
  text-align:center;

  font-weight: 900;
  width:100%;
  bottom: 10%;
  color: #FFF;
  opacity: 0;
  transition: color .6s ease;
}
.portfolio-bg:hover {
  transition: color .6s ease;
  opacity: 1;
}
```  
## Эффект затемнения на изображении  
добавляем слой в html перед классом text-bg:  

```
  <div class="portfolio-layer"></div> 
```  
И стилизуем его:  

```
.portfolio-layer {
    position:absolute;
    width:100%;
    height:100%;
    background:rgba(0,0,0,0.3);
}
```  
