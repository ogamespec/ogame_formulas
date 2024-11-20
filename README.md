# Список формул (и не только) для OGame

Игра делится на две большие "части": экономическая и боевая.

К экономике относится выработка, скорость строительства, исследования, количество и параметры планет и прочие подобные фичи.

К боевой части относится собственно скорость флота, характеристики юнитов и т.п.

⚠️ Классы и формы жизни (ФЖ) не являются отдельной частью, но являются своеобразными "мутаторами" экономики и флота.

🚧 Пока набор рандомных фактов вперемешку с формулами, потом растащим всё по красоте.

## Экономическая часть

TBD.

### Выработка энергии

Энергию вырабатывают:
- Солнечные электростанции
- Термоядерная электростанция
- Солнечный спутник

### Бонусы энергии от домиков ФЖ

![image](https://github.com/user-attachments/assets/1b765845-10c3-4c19-91fc-77a033059959)

На домики ФЖ (вроде камеры разрыва) не действует бонус инженера и другие бонусы вроде Ком. состава. Т.е. эти домики -- сами по себе дают бонус от базовой выработки энергии.

### Куда капает роктальская Т18

На картинке выработка планеты до улучшения Т18 первого уровня и после улучшения. Стрелками показано куда "капнуло":

![image](https://github.com/user-attachments/assets/04a535d4-0904-4f4b-a6fa-30074143ac8b)

Класс накидывает +25% от выработки шахт.
Т18 накидывает к классу: 25 * (1.0 + бонус)

![image](https://github.com/user-attachments/assets/f91b0851-fdbf-4281-aa89-8451eb5b32b0)

Коллектор вкачаный на Т18 +50% даёт: +37.5% шахты, +75% гусянки, +15% больше гусянок

## Боевая система

TBD.

### Восстановление флота при атаке генералом

Часть флота возвращается в док на исходной планете, при следующих условиях:
- На исходной планете имеется док. Если док отсутствует - выведется стандартное предупреждение что "обнаружены повреждения" и попросят построить док (иконка дока вместо иконки атаки) (желательно таки иметь док, т.к. он увеличивает процент восстановления)
- Было уничтожено кораблей на более чем 150.000 ресурсов (150 очей) и не менее чем 5% от суммарной стоимости флота в слоте.

То есть для САБ - условие проверяется для каждого слота по отдельности. Если убито менее чем 5% слота - дозвидання. Если убито более 5% - проверяем что стоимость более 150 очей и если да - то восстанавливаем сколько сможет док на исходной планете.

Старт с луны приравнивается к старту с планеты (как и механика дока во время дефа).

## OGame API

Разработчики добавили возможность краулить некоторые "кишки" игры, используя xml файлы. Некоторые файлы публичные (напр. статистика), а некоторые требуют приватного ключа (доклады).
Приватный ключ получается на форуме OGame Origin, в случае если вы доверенный разработчик. У ключа есть "срок годности".

TBD.
