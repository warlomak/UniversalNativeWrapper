# UniversalNativeWrapper
COM обертка над Native компонентами фирмы 1С, предназначена для использования на платформе 1С 7.7, 8.0 и 8.1, 8.2, 8.3.
Данная обертка позволяет использовать все современные компоненты на устаревшей платформе 1С без необходимости ее обновления.

Компоненту UniversalNativeWrapper.dll необходимо зарегистрировать командой regsvr32
Затем в 1С использовать следующий код:

ПодключитьВнешнююКомпоненту("AddIn.UniversalNativeWrapper");

Драйвер = Новый ("AddIn.UniversalNativeWrapper"); 

Для инициализации Native компоненты необходимо:

Драйвер.УстановитьИмяДрайвера(ПутьДоКомпоненты, ИмяКомпоненты);

Например, для использования Native компоненты для оборудования ШтрихМ, нужно прописать следующий код:

Драйвер.УстановитьИмяДрайвера("E:\Yandex.Disk\YandexDisk\SHTRIHMKKT_NATIVE_32_SMDrvFR1C3.dll", "SMDrvFR1C3");

После этого можно выполнять уже методы присутствующие уже в native объекте, например.

Ревизия = Драйвер.ПолучитьРевизиюИнтерфейса();

Проблемы:

1. На платформе 1С при инициализации обертки происходит утечка памяти (нужно доработать удаление объектов из памяти). На платформе 8.2 и выше это более заметно, и связано с тем,
что для COM компоненты не выгружается из памяти до закрытия 1С, поэтому не вызывается метод Done(), при котором подключенная Native компонента также выгружается из памяти. Удаление
из памяти происходит только при закрытии 1С.
2. Не проверена трансляция и установка свойств Native компоненты, работают только методы.
3. Не знаю как обработать ошибку "Нарушение прав доступа при обращении к памяти", которая может возникать на стороне Native компоненты, try и _try ее почему-то не перехватывают.


🤝 Помощь в разработке приветствуется.
