# GRIx4 - часы на ГРИ и STM32
![PHOTO](https://github.com/AlexGyver/GRIx4_by_KARMAN/blob/master/Photo/Photo4.jpg)

## 1. Техническое описание
Часы цифровые электровакуумные предназначены для отображения текущего значения времени на четырех газоразрядных индикаторах. Основные параметры устройства:
- Габариты печатной платы – 87 х 50 мм;
- Высота устройства – не более 80 мм;
- Напряжение питания – 5 В;
- Ток потребления в режиме индикации времени – не более 250 мА;
- Ток потребления в режиме прожига – не более 300 мА;
## 2. Рекомендации по сборке устройства
### 2.1 Сборка часов
Сборку часов следует проводить в соответствии с приложенными схемами и спецификацией. Конструкция часов предполагает три варианта реализации питания: гальванически изолированное через разъем mini-USB, без гальванической изоляции через разъем mini-USB или через разъем XP4. От выбранного способа питания зависит необходимость установки компонентов G1, R23, R24, XP1 и XP4 (см. раздел «Спецификация»). В начале монтажа платы рекомендуется установить компоненты DD5 и U1, далее установку компонентов следует проводить по мере увеличения их габаритов. В последнюю очередь рекомендуется установить выводные компоненты. При необходимости допускается заменить тактовые кнопки SB1-SB4 на аналогичные по функционалу. В зависимости от выбранного способа загрузки в контроллер исполняемого кода следует установить перемычку BOOT0 (см. раздел «Загрузка и обновление прошивки»). Для установки перемычки достаточно нанести на площадки небольшое количество припоя таким образом, чтобы их замкнуть. Перед установкой индикаторов необходимо смыть остатки флюса отмывочным средством (рекомендуемая смесь: изопропанол и бензин «Калоша» в соотношении 1:1).
### 2.2 Модель индикаторов
В качестве газоразрядных индикаторов рекомендуется использовать индикаторы ИН-16, но при необходимости на плату могут быть установлены индикаторы ИН-14. Во избежание выхода из строя индикаторов необходимо соблюдать их цоколевку (стрелочный указатель на плате и газоразрядном индикаторе указывает на первый вывод). Не рекомендуется запускать часы без установленных индикаторов. После завершения сборки необходимо повторно смыть остатки флюса.
### 2.3 Дополнительная информация
Для предотвращения автоматического сброса времени при отключении часов от питающего напряжения рекомендуется установить элемент питания CR2032 в батарейный отсек XP3. Допускается использовать часы без указанного элемента. Перед первым подключением питания следует проверить цепи на наличие короткого замыкания. Также рекомендуется провести визуальный осмотр платы. При использовании устройства без корпуса следует установить в крепежные отверстия латунные стойки PCHSN-10 (H-L-1000-1600-5-03-1N1W) закрепив их гайками M3.
## 3. Загрузка и обновление прошивки
- Загрузка исполняемого кода может осуществляться двумя способами: с помощью программатора ST-Link V2 или посредством USB-UART преобразователя, подключенного к ПК.
- Загрузка с помощью ST-Link V2. Перед прошивкой должна быть установлена перемычка BOOT0. К разъему XP2 подключается программатор ST-Link в соответствии с указанной распиновкой. На ПК запускается ПО «STM32 ST-LINK Utility». В разделе «Target->Settings…->Reset Mode» необходимо установить режим «Software System Reset». Далее следует перейти в раздел «Target->Program…» и выбрать необходимый файл прошивки. Затем нажатием кнопки «Start» запускается прошивка. После завершения загрузки следует отключить программатор и закрыть ПО.
- Загрузка с помощью USB-UART преобразователя. Перед прошивкой перемычка BOOT0 не должна быть установлена. К разъему XP4 подключается UART преобразователь в соответствии с указанной распиновкой (TXp->RXd и RXp->TXd, где TXp, RXp – выводы преобразователя, а TXd, RXp – выводы устройства). На ПК запускается ПО «Flash Loader Demonstrator». В разделе «Port Name» указывается номер подключенного преобразователя и нажимается «Next». После успешной инициализации устройства необходимо еще два раза нажать кнопку «Next». Далее необходимо выбрать пункт «Download from file» и указать путь к файлу прошивки. Затем следует вновь нажать кнопку «Next» и дождаться окончания загрузки. После завершения загрузки следует отключить программатор, закрыть ПО и установить перемычку BOOT0.
## 4. Управление режимами индикации
### 4.1 Режим отображения времени
Активируется по умолчанию после подключения питания устройства. В случае некорректного отображения следует изменить тип индикатора (см. пункт 4.3)
### 4.2 Режим установки времени
Активируется длительным удержанием центральной кнопки в режиме отображения времени. При переходе в указанный режим два левых индикатора отображения значения часов загораются чуть ярче индикаторов значения минут. Корректировка текущего параметра осуществляется нажатием левой или правой кнопки в меньшую или большую сторону соответственно. При длительном удержании одной из боковых кнопок увеличение или уменьшение параметра будет происходить автоматически с изменением на единицу через небольшие интервалы времени. Переключение между корректируемыми параметрами осуществляется кратковременным нажатием на центральную кнопку. При этом корректируемому параметру соответствует более интенсивное свечение индикаторов. Переключение происходит циклически: часы->минуты->секунды->часы… При корректировке значения секунд два левых индикатора отключаются. Возврат в режим отображения времени осуществляется длительным нажатием на центральную кнопку, при этом яркость индикаторов уравнивается.
### 4.3 Режим изменения типа индикаторов
Активируется длительным удержанием левой или правой кнопки в режиме отображения времени. Удержание левой кнопки соответствует переключению типа двух левых индикаторов, а удержание правой – двух правых индикаторов. Корректному выбору типа индикаторов соответствует индикация нулей в соответствующих индикаторах при дальнейшем удержании кнопки. При этом два других индикатора отключаются. Выход из режима происходит при отпускании удерживаемой кнопки. Установленный тип индикатора записывается в энергонезависимую память контроллера и стирается при повторном изменении типа индикаторов или при обновлении прошивки.
### 4.4 Режим установки скважности ШИМ
Активируется кратковременным нажатием одновременно двух крайних кнопок в режиме отображения времени. На четырех индикаторах отображается значение скважности ШИМ (отсчеты таймера с периодом 1500 ед. при частоте тактирования 36 МГц). Управление значением осуществляется подобным описанному в п. 4.2 образом. Для увеличения яркости необходимо увеличить отображаемое значение. При появлении «фантомных» цифр соседних индикаторов следует уменьшать отображаемое значение до полного пропадания «фантомного» эффекта. Выход из режима установки скважности ШИМ осуществляется кратковременным нажатием на центральную кнопку. При этом установленное значение скважности ШИМ записывается в энергонезависимую память контроллера и стирается при повторном изменении значения или при обновлении прошивки.
### 4.5 Режим прожига «отравленного» катода
Активируется длительным удержанием одновременно двух крайних кнопок в режиме отображения времени. При этом в крайнем левом индикаторе загорается катод, соответствующий цифре «0», а динамическая индикация полностью отключается. Если при переходе в режим прожига загорается другая цифра, следует изменить тип индикатора (см. пункт 4.3). Переключение индикаторов происходит циклически слева направо при нажатии левой кнопки. Выбор «отравленного» катода осуществляется нажатием правой кнопки. При этом возрастает потребление устройства, и увеличивается нагрев силовых элементов схемы (см. результаты температурных исследований). Выход из режима прожига «отравленного» катода осуществляется кратковременным нажатием на центральную кнопку.

## Модель
![PHOTO](https://github.com/AlexGyver/GRIx4_by_KARMAN/blob/master/Photo/Model-top.png)

## Чертёж
![PHOTO](https://github.com/AlexGyver/GRIx4_by_KARMAN/blob/master/Photo/Scale.jpg)

## Схема
![PHOTO](https://github.com/AlexGyver/GRIx4_by_KARMAN/blob/master/Photo/Scheme.jpg)

## Плата
![PHOTO](https://github.com/AlexGyver/GRIx4_by_KARMAN/blob/master/Photo/PCB1.jpg)