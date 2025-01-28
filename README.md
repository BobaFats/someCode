# someCode
Любой код который использовался в проектах

В процессе работы бота, необходимо собирать адреса и плошадь квартиры

Создаём переменные. Проект работал на ES5
var tarifNow;
var tarifBase;
var tarifOptimal;
var tarifMax;
var flag = 1;

//Ищем пробелы, цифры, запятые в ведённом тексте
if($session.number.search(/\d\s/) === -1 && $session.number.indexOf(',') > -1){
    $session.number = $session.number.replace(',', '.');
}
$session.number = Number($session.number);

//Функция для поиска текста и расчёта тарифов 
function baseAdress(){
    if($session.adress.match(/Комсомольский.*141|141.*Комсомольский/gi)){
        $session.adress = "Комсомольский, 141";
         tarifNow = 37.74 * $session.number;
         tarifBase = 64.46* $session.number;
        answerShort()
} else if($session.adress.match(/Комсомольский.*143|143.*Комсомольский/gi)){
        $session.adress = "Комсомольский, 143";
         tarifNow = 38.01 * $session.number;
         tarifBase = 67.97* $session.number;
        answerShort()
} else if {
    //И так далее
} else {
    $session.adress = "Не смог сделать расчет. Возможно, допущена ошибка или вашего адреса нет в списке"
    //пушим текст в виджет
    $response.replies = $response.replies || [];
            $response.replies.push({
                "type": "text",
                "text": "Не смог сделать расчет. Возможно, допущена ошибка или вашего адреса нет в списке"
            });
}}

function answerLong(){
    $response.replies = $response.replies || [];
            $response.replies.push({
                "type": "text",
                "text": "Текущий тариф - " + tarifNow.toFixed(2) + " руб/мес.\nПредлагаемый 'Базовый' тариф с весны 2025 - " + tarifBase.toFixed(2) + " руб/мес.\n'Базовый' + пакет 'Оптимальный' - " + tarifOptimal.toFixed(2) + " руб/мес.\n'Базовый' + пакет 'Максимальный' - " + tarifMax.toFixed(2) + " руб/мес." 
            });
}
function answerShort(){
    $response.replies = $response.replies || [];
            $response.replies.push({
                "type": "text",
                "text": "Текущий тариф - " + tarifNow.toFixed(2) + " руб/мес.\nПредлагаемый 'Базовый' тариф с весны 2025 - " + tarifBase.toFixed(2) + " руб/мес." 
            });
}

if($session.adress.match(/свободы.*77|77.*свободы/gi)){
    $session.adress = "Свободы, 77";
     tarifNow = 48.75 * $session.number;
     tarifBase = 79.17 * $session.number;
     tarifOptimal = 84.3 * $session.number;
     tarifMax = 119.3 * $session.number;
    answerLong()
} else if($session.adress.match(/Eреванская.*34|34.*Ереванская/gi)){
    $session.adress = "Ереванская, 34";
     tarifNow = 29.81 * $session.number;
     tarifBase = 68.76 * $session.number;
     tarifOptimal = 79.49 * $session.number;
     tarifMax = 89.9 * $session.number;
    answerLong()
} else if {
  и так далее
}
} else {
  baseAdress()
}
