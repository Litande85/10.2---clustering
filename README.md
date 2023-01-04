# Домашнее задание к занятию "10.2 Кластеризация" - `Елена Махота`

- [Ответ к Заданию 1](#1)
- [Ответ к Заданию 2](#2)
- [Ответ к Заданию 3](#3)
- [Ответ к Заданию 4](#4)
- [Ответ к Заданию 5](#5)
- [Ответ к Заданию 6*](#6)


---

### Задание 1. 

В чем различие между SMP и MPP системами?

*Приведите ответ в свободной форме.*


### *<a name="1">Ответ к Заданию 1</a>*

**SMP (Symmetric Multiprocessing)** – симметричная многопроцессорная архитектура. Главной особенностью систем с архитектурой SMP является наличие общей физической памяти, разделяемой всеми процессорами. Cильно связанные  архитектуры вычислительных систем.

**MPP (Massive Parallel Processing)**– массивно-параллельная архитектура. Главная особенность такой архитектуры состоит в том, что память физически разделена. Cлабо связанные архитектуры вычислительных систем.

*Сравнительная таблица*

|                               | **SMP**                                           | **MPP**                                                 |
|--------------------------------------|---------------------------------------------------|---------------------------------------------------------|
| **память**                           | наличие общей физической памяти                   | память физически разделена                              |
| **ОС**                              | обычно единая ОС                                  | ОС в каждом модуле                                      |
| **масштабируемость**                 | системы с общей памятью плохо масштабируются      | хорошая масштабируемость                                |
| **скорость межпроцессорного обмена** | выше                                              | ниже                                                    |
| **процессоры**                       | тесно связанные                                   | слабосвязанные                                          |
| **примеры использования**            | много пользователей работают с одной базой данных | аналитика для больших объемов распределенных баз данных | 


Использованные источники:
- [Презентация "Отказоустойчивость: Кластеризация", Александр Зубарев](https://u.netology.ru/backend/uploads/lms/attachments/files/data/33431/SRLB-9__%D0%9A%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F.pdf)
- https://intuit.ru/studies/courses/45/45/lecture/1340 
- https://www.techtarget.com/searchdatacenter/tip/Learn-the-difference-between-SMP-vs-MPP


---

### Задание 2.

В чем отличие сильно связанных и слабо связанных систем?

*Приведите ответ в свободной форме.*

### *<a name="2">Ответ к Заданию 2</a>*

**Сильно связанные системы**

Сильно связанная система состоит из нескольких однородных процессоров и массива общей памяти (обычно из нескольких независимых блоков). 

Примеры таких систем: 

● SMP (cимметричные мультипроцессоры),

● NUMA (системы с неоднородным доступом к памяти).

*Схематический вид SMP архитектуры*

![SMP](img/img2023-01-04%20120151.png)

Память служит, в частности, для передачи сообщений между процессорами, при этом все  устройства при обращении к ней имеют равные права и одну и ту же адресацию для всех ячеек памяти. Поэтому SMP-архитектура называется симметричной. Последнее обстоятельство позволяет очень эффективно обмениваться данными с другими  устройствами. SMP-система строится на основе высокоскоростной системной шины.

SMP-системы имеют плохую масштабируемость, так как шина способна обрабатывать только один процесс в каждый момент, вследствие чего возникают проблемы разрешения конфликтов при одновременном обращении нескольких процессоров к одним и тем же областям общей физической памяти. Вычислительные элементы начинают друг другу мешать.

Для построения масштабируемых систем на базе SMP используются кластерные или NUMA-архитектуры.

**Слабо связанные системы**

В слабо связанных системах вся память распределена между процессорными элементами. 

Примеры таких систем:

● системы с массовым параллелизмом (MPP),

● кластерные системы

*Схематический вид MPP архитектуры*

![MPP](img/img2023-01-04%20120152.png)

MPP система строится из отдельных модулей, содержащих процессор, локальный банк операционной памяти (ОП), коммуникационные процессоры (рутеры) или сетевые адаптеры, иногда – жесткие диски и/или другие устройства ввода/вывода. По сути, такие модули представляют собой полнофункциональные компьютеры. Доступ к банку ОП из данного модуля имеют только процессоры (ЦП) из этого же модуля. Модули соединяются специальными коммуникационными каналами. Пользователь может определить логический номер процессора, к которому он подключен, и организовать обмен сообщениями с другими процессорами. Используются два варианта работы операционной системы (ОС) на машинах MPP-архитектуры. В одном полноценная операционная система (ОС) работает только на управляющей машине (front-end), на каждом отдельном модуле функционирует сильно урезанный вариант ОС, обеспечивающий работу только расположенной в нем ветви параллельного приложения. Во втором варианте на каждом модуле работает полноценная UNIX-подобная ОС, устанавливаемая отдельно.

Главным преимуществом систем с раздельной памятью является хорошая масштабируемость: в отличие от SMP-систем, в машинах с раздельной памятью каждый процессор имеет доступ только к своей локальной памяти, в связи с чем не возникает необходимости в потактовой синхронизации процессоров. 

Кластерные вычислительные системы относятся к слабосвязанным системам:

● формируют единый вычислительный ресурс,

● создают иллюзию наличия единственной вычислительной машины.
Каждый узел способен работать автономно. Узел может быть SMP, MPP или однопроцессорной ВМ.


Использованные источники:
- [Презентация "Отказоустойчивость: Кластеризация", Александр Зубарев](https://u.netology.ru/backend/uploads/lms/attachments/files/data/33431/SRLB-9__%D0%9A%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F.pdf)
- https://studfile.net/preview/5171135/page:149/

---

### Задание 3.

Какие преимущества отличают кластерные системы от обычных серверов?

*Приведите ответ в свободной форме.*

### *<a name="3">Ответ к Заданию 3</a>*


Кластерные системы отличаются следующими достоинствами.
* Высокая вычислительная мощность.
* Большая надежность, отказоустойчивость. При отказе компьютера, входящего в кластер, используются ресурсы прочих серверов из того же кластера.
* Высокая масштабируемость. В случае если нагрузка на кластер возрастет, в него просто добавляют еще один сервер.
* Возможность перераспределения ресурсов серверов. Можно сделать кластер для серверов приложений и другой кластер — для серверов БД. Далее, в случае, если нагрузка на сервер БД будет выше, чем предполагалось, то рассматривается вопрос о передаче одного сервера из первого кластера во второй или даже вопрос о совместном использовании одной или нескольких машин в двух кластерах.
высокий коэффициент готовности,
* соотношение цена/производительность,
* можно строить кластер из любых строительных блоков: чем проще и стандартнее блоки, тем дешевле обходится 
вычислительная мощность.

Использованные источники:
- [Презентация "Отказоустойчивость: Кластеризация", Александр Зубарев](https://u.netology.ru/backend/uploads/lms/attachments/files/data/33431/SRLB-9__%D0%9A%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F.pdf)
- https://studref.com/351196/informatika/ispolzovanie_klasterov


---

### Задание 4.

Приведите примеры типов современных кластерных систем?

*Приведите ответ в свободной форме.*


### *<a name="4">Ответ к Заданию 4</a>*



---

### Задание 5.

Где использует сервис Kafka, rabitMQ?

*Приведите ответ в свободной форме.*


### *<a name="5">Ответ к Заданию 5</a>*


---

## Дополнительные задания (со звездочкой*)
Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

---

### Задание 6*.

Исследуйте построение кластера на основе rabbitMQ https://github.com/ypereirareis/docker-rabbitmq-ha-cluster. 
Используя docker-compose? соберите инфраструктуру. Исследуйте ее работы.

Ответьте на следующие вопросы:

- на каких компонетах развернут кластер?
- назначение компонентов кластера?
- какие тесты можно провести для анализа работы кластера?

*Приведите в пример скришоты работающей системы и ответы на вопросы.*

### *<a name="6">Ответ к Заданию 6*</a>*
