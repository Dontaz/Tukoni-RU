# Инструкция для будущих людей по переводу игры «Tukoni: Forest Keepers»

## Содержание

- [Инструкция для будущих людей по переводу игры «Tukoni: Forest Keepers»](#инструкция-для-будущих-людей-по-переводу-игры-tukoni-forest-keepers)
  - [Содержание](#содержание)
  - [Нужные программы](#нужные-программы)
  - [Этап 1. Перевод текста](#этап-1-перевод-текста)
  - [Этап 2. Перевод логотипа игры](#этап-2-перевод-логотипа-игры)
    - [Этап 2.1. Делаем дамп памяти](#этап-21-делаем-дамп-памяти)
    - [Этап 2.2. Создаём mapping (.usmap) файл для игры](#этап-22-создаём-mapping-usmap-файл-для-игры)
    - [Этап 2.3. Вытаскиваем текстуру логотипа из игры](#этап-23-вытаскиваем-текстуру-логотипа-из-игры)
    - [Этап 2.4. Рисуем свой логотип](#этап-24-рисуем-свой-логотип)
    - [Этап 2.5. Из «.png» в «.uasset»](#этап-25-из-png-в-uasset)
    - [Этап 2.6. Запаковываем «.uasset» в мод-файл для игры](#этап-26-запаковываем-uasset-в-мод-файл-для-игры)

## Нужные программы

- [FModel](https://github.com/4sval/FModel)
- [jmap dumper](https://github.com/trumank/jmap)
- [UnrealReZen](https://github.com/rm-NoobInCoding/UnrealReZen)
- [UE4-DDS-Tools](https://github.com/matyalatte/UE4-DDS-Tools) (версию с GUI)
- [PowerShell](https://github.com/powershell/powershell)
- Любая программа для открытия «.csv» файлов. Рекомендую [Modern CSV](https://www.moderncsv.com/)

## Этап 1. Перевод текста

1. Текст в игре лежит в открытую по пути: «Tukoni Forest Keepers / TukoniForestKeepers / Content / Localization / Custom / Tukoki Forest Keepers—Game Localization.csv»;
2. Откройте файл «Tukoki Forest Keepers—Game Localization.csv»;
3. В стоблце «Language-En» переводим весь текст, саму ячейку «Language-En» переводить не нужно (т.е. не нужно писать в этой ячейке «Язык-Ру»);
4. Действие выше заменит английский текст в игре на ваш, можете перевести другой язык, не обязательно английский заменять;
5. Текст готов и его можно сразу заменить в игре путём простого перемещения модифицированного файла «Tukoki Forest Keepers—Game Localization.csv» в папку «Tukoni Forest Keepers / TukoniForestKeepers / Content / Localization / Custom».

## Этап 2. Перевод логотипа игры

### Этап 2.1. Делаем дамп памяти

1. Открываем Task Manager (Диспетчер задач) в Windows;
2. Запускаем игру и в Task Manager ищем процесс игры «TukoniForestKeepers»;
3. Кликаем правой кнопкой мыши (ПКМ) по процессу игры и выбираем в списке «Create memory dump file», на выходе будет файл «TukoniForestKeepers-Win64-Shipping.DMP»;
4. Переместите файл «TukoniForestKeepers-Win64-Shipping.DMP» в папку с программой «jmap_dumper.exe».

### Этап 2.2. Создаём mapping (.usmap) файл для игры

1. Откройте папку с «jmap_dumper.exe» в PowerShell (можно через ПКМ по пустому месту внутри папки с «jmap_dumper.exe» и выбрать «Open in Terminal»);
2. Используйте команду:

```shell
.\jmap_dumper.exe --minidump "TukoniForestKeepers-Win64-Shipping.DMP" TukoniForestKeepers.usmap
```

1. На выходе в этой папке появится mapping файл «TukoniForestKeepers.usmap»

### Этап 2.3. Вытаскиваем текстуру логотипа из игры

1. Откройте программу «FModel.exe»;
2. Слева-сверху нажмите на «Directory» → «Selector»;
3. Напротив «Directory» укажите путь к папке с игрой;
4. Напротив «UE Versions» выберите «GAME_UE5_4»;
5. В «Game Archives» выберите «TukoniForestKeepers-Windows.utoc»;
6. Откройте «TukoniForestKeepers» → «Content» → «Textures» → «MainMenu»;
7. В «MainMenu» найдите файл «Tukoni-Forest-Keepers_Logo_EN.uasset»;
8. Откройте «Settings» вверху программы;
9. В «General» поставьте галочку напротив «Local Mapping File (drag & drop)»;
10. Ниже появится поле «Mapping File Path»;
11. В поле «Mapping File Path» либо через «$\dots$» найдите ваш файл «TukoniForestKeepers.usmap» из папки с «jmap_dumper.exe», либо перетащите файл «TukoniForestKeepers.usmap» в поле «Mapping File Path». Нажмите «OK»;
12. Нажмите ПКМ по «Tukoni-Forest-Keepers_Logo_EN.uasset»;
13. Выберите «Export» и сделайте два экспорта:
    1.  «Raw Data (.uasset)» и
    2.  «Textures» (если кнопка неактивна, то попробуйте перезапустить программу «FModel»).
14. Файлы экспортируются в папку «Output», которая находится рядом с файлом «FModel.exe»;
15. Внутри папки «Output» по пути «Output / Exports / TukoniForestKeepers / Content / Textures / MainMenu» будет два файла «Tukoni-Forest-Keepers_Logo_EN.png» и «Tukoni-Forest-Keepers_Logo_EN.uasset».

### Этап 2.4. Рисуем свой логотип

1. Возьмите файл «Tukoni-Forest-Keepers_Logo_EN.png» и можете его редактировать как угодно, но обязательно не меняйте название файла и разрешение изображения — «1280 $\times$ 720».

### Этап 2.5. Из «.png» в «.uasset»

1. Откройте папку с программой «UE4-DDS-Tools»;
2. Запустите программу через «GUI.exe»;
3. В поле «Uasset file» вставьте файл «Tukoni-Forest-Keepers_Logo_EN.uasset»;
4. В поле «Texture file (dds, tga, hdr, png, jpg, or bmp)» вставьте ваш новый файл «Tukoni-Forest-Keepers_Logo_EN.png»;
5. В поле «Output folder» можете оставить «injected»;
6. В поле «UE version» поставьте «5.4»;
7. Галочки внизу поставьте только у «Skip non-texture assets» и «Use cubic filter»;
8. Нажмите «Inject», а когда выйдет окно с «Success» — можете закрыть программу;
9. Рядом с «GUI.exe» появится папка «injected» с файлом «Tukoni-Forest-Keepers_Logo_EN.uasset» внутри.

### Этап 2.6. Запаковываем «.uasset» в мод-файл для игры

1. Подготовьте файл «Tukoni-Forest-Keepers_Logo_EN.uasset»:
   1. Создайте папку с названием мода, например, «TukoniFK_RussianLanguage_P»;
   2. Откройте папку «TukoniFK_RussianLanguage_P» и воссоздайте путь файлов игры, т.е. внутри папки «TukoniFK_RussianLanguage_P» создайте папку «TukoniForestKeepers», внутри которой создайте папку «Content», внутри которой создайте папку «Textures», внутри которой создайте папку «Content», внутри которой создайте папку «MainMenu», в которую скопируйте файл «Tukoni-Forest-Keepers_Logo_EN.uasset».
2. Откройте папку с программой «UnrealReZen»;
3. Откройте папку с «UnrealReZen.exe» в PowerShell (можно через ПКМ по пустому месту внутри папки с «UnrealReZen.exe» и выбрать «Open in Terminal»);
4. Используйте команду:

```shell
.\UnrealReZen.exe --game-dir "Путь к игре" --content-path "Путь к папке с модом" --engine-version GAME_UE5_4 --output-path "TukoniFK_RussianLanguage_P.utoc"
```

где: 
- вместо «"Путь к игре"» укажите папку с игрой, например «"F:\Games\Tukoni Forest Keepers"» (кавычки «"» не убирайте);
- вместо «"Путь к папке с модом"» укажите папку с модом, например, «"C:\Users\user\Desktop\TukoniFK_RussianLanguage_P"» (кавычки «"» не убирайте);
- вместо «"TukoniFK_RussianLanguage_P.utoc"» можете вписать своё название мода, но не убирайте  кавычки «"» и сохраните в конце «.utoc».

5. Когда в PowerShell выйдет «Done! 1 file(s) packed», можете закрывать PowerShell;
6. В папке с программой «UnrealReZen» появится три файла с названием вашего мода (например, TukoniFK_RussianLanguage_P) с расширениями «.pak», «.ucas» и «.utoc»;
7. Эти три файла переместите в папку «Paks», которую можно найти по пути «Tukoni Forest Keepers / TukoniForestKeepers / Content».

<br><br>

<div align = "center">

≽^•⩊•^≼

ВСЁ ГОТОВО

</div>