## Сравнение реализаций биквадратных фильтров

Блокноты jupyter/Google Collab для сравнения пведения реализаций цифровых фильтров на арифметике с фиксированными точками
* Сравниваются 2 способа релизации: Прямая форма 1 (Direct Form 1, DF1) и сопряженная форма (Coupled Form, Gold-Raider form)
* Учтены эффекты квантования коэффициентов, квантования переменных состояний и сигналов, способы округления, переполнение переменных сотяония (насыщение). 

### Состав

* **`fixpt.py`** --- библиотека фиксированныз точек
  * `SaturationPolicy`, `QuantPolicy` --- декларации поведения при насыщении (переполнение, насыщение, исключение) и квантовании (`Truncate`, `TruncateToZero`, `Round`)
  * `FixedPoint` --- абстрагирует переменную с фиксированно точкой с фиксированной разрядностью, дробной частью способом насыщения и квантования.
  * При вычислениях промежуточные результаты хранятся в переменных типа `FixedPointBase`, представляющем числа с фиксированной точкой произвольной точности.
  * Прменение политик насыщение и квантования происходит только при присвоении значений типам `FixedPoint`.
* **`biquad_filters.py`** ---  реализация фильтров `BiQuadDF1`, `BiQuadCoupled`.
  * BiQuadDF1.Config --- конфигурация бока ПЛИС согласно HWH (разрадности, способ округления).
  * BiQuadDF1.Registers --- значения регистров и процедуры их вычисления из числителя и знаменателя передаточной функции.
  * BiQuadDF1 --- непосредственно реализация ПФ с методом output() для симуляции.
* **`test_biquad.ipynb`** --- блокнот-демонстрация.
   * Назаначение парметров блоков
   * Синтез фильтров разного типа.
   * Сравнение с реализацие с плавающими точками (моделирвоание, диаграмма Боде)
* **`test_biquad_collab.ipynb`** --- блокнот-демонстрация для GoogleCollab
   * Запуск блокнота: https://colab.research.google.com/github/EPC-MSU/biquad_filters_comparison/blob/master/test_biquad_collab.ipynb
   * Функционал аналогичен attachment:test_biquad.ipynb 
