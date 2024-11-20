# Список формул (и не только) для OGame

Игра делится на две большие "части": экономическая и боевая.

К экономике относится выработка, скорость строительства, исследования, количество и параметры планет и прочие подобные фичи.

К боевой части относится собственно скорость флота, характеристики юнитов и т.п.

⚠️ Классы и формы жизни (ФЖ) не являются отдельной частью, но являются своеобразными "мутаторами" экономики и флота.

🚧 Пока набор рандомных фактов вперемешку с формулами, потом растащим всё по красоте.

⚠️ Раздел в стадии заполнения, поэтому могут быть косячки какие-то. Со временем исправятся.

## Экономическая часть

TBD.

### Естественное производство

Это примитивная выработка любой планеты, даже без шахт.
```
металл = 30 * Скорость_Эко * Бонус_позиции
кристалл = 15 * Скорость_Эко * Бонус_позиции
```

Как видно, на естественное производство влияет скорость экономики, а также бонус за позицию планеты (на позициях 1-3 повышенная выработка кристалла, на позициях 7-9 повышенная выработка металла).
Естественное производство не добавляется к базовой выработке шахт и на него не действуют(?) бонусы выработки.

В версии 0.84 естественное производство было 20/10.

### Выработка энергии

Энергию вырабатывают:
- Солнечные электростанции
- Термоядерная электростанция
- Солнечный спутник

### Бонусы энергии от домиков ФЖ

![image](https://github.com/user-attachments/assets/1b765845-10c3-4c19-91fc-77a033059959)

На домики ФЖ (вроде камеры разрыва) не действует бонус инженера и другие бонусы вроде Ком. состава. Т.е. эти домики -- сами по себе дают бонус от базовой выработки энергии. Это логично, т.к. они не производят энергию.

### Куда капает роктальская Т18

На картинке выработка планеты до улучшения Т18 первого уровня и после улучшения. Стрелками показано куда "капнуло":

![image](https://github.com/user-attachments/assets/04a535d4-0904-4f4b-a6fa-30074143ac8b)

Класс накидывает +25% от выработки шахт.
Т18 накидывает к классу: 25 * (1.0 + бонус), например для бонуса Т18 0.2% получится 25 * 1.002 = 25.05%.

![image](https://github.com/user-attachments/assets/f91b0851-fdbf-4281-aa89-8451eb5b32b0)

Коллектор вкачаный на Т18 +50% даёт: +37.5% шахты, +75% гусянки, +15% больше гусянок

### Гусеничники

```
Гусеничников_Макс = Ceil (Уровень_шахты_металла + Уровень_шахты_кристалла + Уровень_синтезатора дейтерия * Фактор)
```

`Фактор` для большинства вселенных равен 8.

Если на планете построено больше чем `Гусеничников_Макс`, то остальные просто игнорируются до тех пор пока не будут прокачаны шахты и `Гусеничников_Макс` не изменится.

Если класс игрока Коллекционер И активен Геолог, то Гусеничников_Макс нужно умножить на 1.1  (на 10% больше). На этот бонус влияет Т18 для Коллектора.

Пример: класс Коллектор + активен Геолог, шахты 42-34-36. Гусеничников_Макс = (42 + 34 + 36) * 8 * 1.1 = 985,6 (985).

Выработка:
```
Базовый бонус гусеничников: выработка шахты * 0.0002 * активных гусеничников
Затем бонус умножается на "прожарку" (1.1 - 1.5)
Затем умножается на бонус увеличенной выработки: для коллектора это 0.5 модифицированный Т18, для всех остальных классов - считается от техи ФЖ на гусей, которая имеет кап 0.5)
```
Пример см. ниже.

Фактор выработки гусеничников 0.0002 - скрытая настройка сервера `resourceBuggyProductionBoost`

Потребление энергии: 1 гусеничник потребляет 50 энергии (скрытая настройка сервера `resourceBuggyEnergyConsumptionPerUnit`)

Перегрузка: у коллектора есть возможность установить выработку/потребление до 150% (110, 120, 130, 140 или 150). В этом случае базовая выработка гусеничников умножается на 1.1-1.5 (110%-150%).

Пример расчёт выработки гусеничников (не сошлось на 5(!) единиц мета), где не пойму:

![image](https://github.com/user-attachments/assets/1864a42f-88c7-4adc-bf32-1f687c6b9508)

(если подставить крис и дейт то всё хорошо)


### Уровень бонуса опыта формы жизни

Уровень прокачки ФЖ влияет на все остальные формулы (экономика/флот).

Суть такая - что бонус опыта соответсвующей расы ФЖ мультипликативно действет на все исследования ФЖ на планете где выбрана эта раса. Пример:

![image](https://github.com/user-attachments/assets/252d84b3-acaa-4d13-9650-b99bdf3c89df)

- Бонус опыта рокталов: 4.3%
- Бонус за второй уровень Т18 улучшения Коллектора: 0.4%
- Итоговое улучшение Т18 техи получается такое: 0.4 * 1.043 = 0.4172 (0.41%)

Ещё раз: бонус опыта ФЖ действует ТОЛЬКО на планеты соответствующей расы, например на планетах где выбраны рокталы - действует бонус опыта для рокталов. Прокачать опыт можно не более 100 УР (+10% макс.)

## Боевая система

TBD.

### Восстановление флота при атаке генералом

Часть флота возвращается в док на исходной планете, при следующих условиях:
- На исходной планете имеется док. Если док отсутствует - выведется стандартное предупреждение что "обнаружены повреждения" и попросят построить док (иконка дока вместо иконки атаки) (желательно таки иметь док, т.к. он увеличивает процент восстановления)
- Было уничтожено кораблей на более чем 150.000 ресурсов (150 очей) и не менее чем 5% от суммарной стоимости флота в слоте.

То есть для САБ - условие проверяется для каждого слота по отдельности. Если убито менее чем 5% слота - дозвидання. Если убито более 5% - проверяем что стоимость более 150 очей и если да - то восстанавливаем сколько сможет док на исходной планете.

Старт с луны приравнивается к старту с планеты (как и механика дока во время дефа).

### Луны

Формула уничтожения луны и взрыва ЗС:

![image](https://github.com/user-attachments/assets/13c88940-2432-4a7c-ae7d-2e3e21865413)


## OGame API

Разработчики добавили возможность краулить некоторые "кишки" игры, используя xml файлы. Некоторые файлы публичные (напр. статистика), а некоторые требуют приватного ключа (доклады).
Приватный ключ получается на форуме OGame Origin, в случае если вы доверенный разработчик. У ключа есть "срок годности".

Пример ссылки для получения настроек сервера: https://s198-ru.ogame.gameforge.com/api/serverData.xml

Источник: https://board.origin.ogame.gameforge.com/index.php/Thread/3927-OGame-API/?s=ffcc1c47d6c393b72b2f12b17368e753156b20b8
