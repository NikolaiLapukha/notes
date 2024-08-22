## Обработка событий нескольких элементов через их родителя

```js
let elementDude = document.getElementById("theDude");//Получение элемента родителя
//Вешаем прослушиватель на элемент родителя
elementDude.addEventListener("click", (e)=>{
  if(e.target != e.currentTarget){//Проверяем не является ли текущий элемент элементом родителя
    if(e.target.id === "one"){//Проверка какой именно это потомок
      console.log("one");//Код для определенного потомка
    }
    else if(e.target.id === "two"){
      console.log("two");
    }
    else if(e.target.id === "three"){
      console.log("three");
    }
    else{
      console.log("Another element!");
    }
  }
  e.stopPropagation();//Прекращение всплытия события дальше элемента на котором оно навешано
},false);
```