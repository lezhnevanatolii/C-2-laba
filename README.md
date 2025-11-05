# C-2-laba
STL
Лабораторная работа №2.
Задание 1. Заполнение и доступ к элементам. Обратные итераторы.
Дан набор целых чисел с четным количеством элементов. Заполнить дек D исходными числами, вывести первую половину элементов дека D в обратном порядке, а затем — вторую половину (также в обратном порядке).
Алгоритм решения задачи
1.	Имеется набор целых чисел с четным количеством элементов.
2.	Заполнить дек D исходными числами — можно с помощью конструктора, использующего итераторы из массива (или вектора).
3.	Определить половину длины дека.
4.	Вывести первую половину элементов дека в обратном порядке.
5.	Вывести вторую половину элементов дека в обратном порядке.
Структура кода
•	Объявление и инициализация исходного набора (например, вектор целых чисел).
•	Создание дека D из этого набора.
•	Расчет половины size/2.
•	Использование обратных итераторов rbegin() и rend() для вывода частей дека в обратной последовательности:
•	Первая половина — от rbegin() до rbegin() + half.
•	Вторая половина — от rbegin() + half до rend().
•	Вывод с форматированием.
Тест для проверки работы программы
Исходные данные:
plaintext
{1, 2, 3, 4, 5, 6, 7, 8}
Ожидаемый результат:
Первая половина (в обратном порядке): 4 3 2 1
Вторая половина (в обратном порядке): 8 7 6 5
Полный код программы
cpp
#include <iostream>
#include <deque>
#include <vector>

int main() {
        std::vector<int> nums = {1, 2, 3, 4, 5, 6, 7, 8}; 

        std::deque<int> D(nums.begin(), nums.end());

    int size = D.size();
    int half = size / 2;

    std::cout << "Первая половина (в обратном порядке): ";
    for (auto rit = D.rbegin(); rit != D.rbegin() + half; ++rit) {
        std::cout << *rit << " ";
    }
    std::cout << std::endl;

    
    std::cout << "Вторая половина (в обратном порядке): ";
    for (auto rit = D.rbegin() + half; rit != D.rend(); ++rit) {
        std::cout << *rit << " ";
    }
    std::cout << std::endl;

    return 0;
}
Задание 2. Вставка элементов
Дан вектор V. Вставить после каждого элемента исходного вектора число − 1. Использовать функцию-член insert в цикле с параметром-итератором. Указание. Организуйте перебор элементов вектора в цикле с параметром-итератором i. Вставку выполняйте в позицию ++i, обязательно присваивая параметру i значение, возвращаемое функцией-членом insert.
Алгоритм решения
1.	Имеется исходный вектор V.
2.	Перебираем его элементы с помощью итератора i.
3.	Для каждого элемента:
•	Переходим к следующей позиции ++i.
•	Вставляем число -1 после текущего элемента с помощью insert.
•	insert возвращает итератор на вставленный элемент. Обновляем i этим итератор.
•	Потом делаем ++i, чтобы перейти к следующему исходному элементу (после вставки).
Структура кода
•	Объявление исходного вектора V.
•	Итерирование по V с помощью while и итератора i.
•	Вставка -1 после каждого элемента через insert.
•	Обновление i после вставки.
•	Вывод итогового вектора.
Тест на корректность
Исходный вектор:
1 2 3 4 5
После вставки:
1 -1 2 -1 3 -1 4 -1 5 -1
Полный код программы
cpp
#include <iostream>
#include <vector>

int main() {
   
    std::vector<int> V = {1, 2, 3, 4, 5};

    auto i = V.begin();

    while (i != V.end()) {
        
        i = V.insert(++i, -1);
     
        ++i;
    }

        for (const auto& elem : V) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
Задание 3. Удаление элементов
Дан дек D с нечетным количеством элементов N (≥3). Удалить средний элемент дека. Использовать функцию-член erase.
Алгоритм решения:
1.	Иметь дек D с нечетным количеством элементов N (нужно проверить, что N >= 3 и N нечетное).
2.	Определить позицию среднего элемента — это индекс N/2.
3.	Получить итератор на этот элемент (D.begin() + N/2).
4.	Удалить средний элемент с помощью функции-члена erase.
5.	Вывести остаточный дек.
Структура кода:
•	Объявление и инициализация дека D.
•	Вычисление размера N и проверка условий.
•	Получение итератора на средний элемент.
•	Удаление среднего элемента.
•	Вывод результата.
Тест:
•	Входной дек: {10, 20, 30, 40, 50}
•	После удаления среднего: {10, 20, 40, 50}
•	Проверка работы при различных значениях.
Полный код:
cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> D = {10, 20, 30, 40, 50};
    int N = D.size();

    if (N >= 3 && N % 2 == 1) {
        auto midIt = D.begin() + N / 2;
        D.erase(midIt);
    }

    for (const auto& elem : D) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
Задание 4. Итераторы и алгоритмы.
Дана строка name и целое число K (> 0). Записать в текстовый файл с именем name K символов «*». Использовать алгоритм fill_n.
Алгоритм решения:
1.	Получить имя файла (name) и число символов (K).
2.	Открыть файл с этим именем для записи.
3.	Проверить успешность открытия файла.
4.	Создать итератор для вывода в файл (ostream_iterator<char>).
5.	Использовать функцию fill_n, чтобы записать в файл K символов ' * '.
Структура кода:
•	Ввод name и K.
•	Открытие файла для записи.
•	Проверка успешности открытия.
•	Использование fill_n с ostream_iterator для записи символов ' * ' в файл.
Тест:
•	Ввод: test.txt 5
•	В результате в файле test.txt содержится: *****
Полный код:
cpp
#include <iostream>
#include <fstream>
#include <iterator>
#include <algorithm>

int main() {
    std::string name;
    int K;
    std::cin >> name >> K;

    std::ofstream outFile(name);
    if (!outFile) {
        std::cerr << "Не удалось открыть файл для записи." << std::endl;
        return 1;
    }

    std::ostream_iterator<char> outIter(outFile);
    std::fill_n(outIter, K, '*');

    return 0;
}
Задание 5. Алгоритмы поиска.
Даны вектор V и список L; вектор V имеет четное количество элементов. Продублировать последний элемент списка, совпадающий с каким-либо элементом из первой половины исходного вектора. Если список не содержит требуемых элементов, то не изменять его. Использовать алгоритм find_first_of и функцию-член insert для списка.
Алгоритм решения:
1.	Найти первую половину элементов вектора V (V.begin() до V.begin() + half).
2.	Обойти список L в обратном порядке (rbegin() до rend()), чтобы найти последний элемент, совпадающий с любым из элементов первой половины.
3.	Используя find_first_of, искать совпадение между текущим элементом L и первой половиной V.
4.	Как только найдено последнее совпадение, преобразовать обратный итератор в обычный и вставить после него дубликат элемента (insert) с помощью insert.
Структура кода:
1.	Объявление исходных данных V и L.
2.	В цикле по списку в обратном порядке ищем совпадение с первой половиной V с помощью find_first_of.
3.	После нахождения последнего совпадения вставляем его дубликат.
4.	Выводим итоговой список.
Тест:
•	Вектор V = {1, 2, 3, 4, 5, 6}
•	Список L = {0, 3, 7, 2, 8}
•	Первые половина V = {1, 2, 3}
•	Последний совпадающий элемент в списке — это 2 (подходит последний раз).
•	После вставки список будет: {0, 3, 7, 2, 2, 8}.
Полный код:
cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

int main() {
    std::vector<int> V = {1, 2, 3, 4, 5, 6};
    std::list<int> L = {0, 3, 7, 2, 8};

    int n = V.size();
    int half = n / 2;

    typename std::list<int>::iterator lastFoundIt = L.end();
    bool found = false;

    for (auto it = L.rbegin(); it != L.rend(); ++it) {
        auto result = std::find_first_of(V.begin(), V.begin() + half, it, std::next(it));
        if (result != V.begin() + half) {
            lastFoundIt = std::prev(it.base());
            found = true;
            break;
        }
    }

    if (found) {
        L.insert(std::next(lastFoundIt), *lastFoundIt);
    }

    for (const auto& elem : L) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
Задание 6. Базовые модифицирующие алгоритмы. Итераторы вставки.
Дано число K (0 <K< 10) и списки L1 и L2, каждый из которых содержит не менее 10 элементов. Выполнить для списка L1 циклический сдвиг элементов вправо на K позиций, а для списка L2 — циклический сдвиг влево на K позиций. Использовать алгоритм rotate и функцию advance.
 АЛГОРИТМ РЕШЕНИЯ
1.	Определение величины сдвига: Вычисляем фактический сдвиг через K % size для обработки случаев, когда K > размера списка
2.	Выбор направления сдвига:
o	Правый сдвиг: middle = начало + (размер - сдвиг)
o	Левый сдвиг: middle = начало + сдвиг
3.	Использование advance: Перемещение итератора на нужную позицию
4.	Применение rotate: Переупорядочивание элементов списка относительно выбранной средней точки
Пример для L1 = {1,2,3,4,5,6,7,8,9,10}, K=3:
•	Правый сдвиг: middle = begin() + (10 - 3) = begin() + 7
•	rotate(begin, begin+7, end): {8,9,10,1,2,3,4,5,6,7}
СТРУКТУРА КОДА
text
Copy
Download
cyclic_rotate/
Основная логика
cyclicRotate() - универсальная функция сдвига
Вычисление реального сдвига
Определение средней точки
Применение std::rotate
Инициализация данных
Список L1
Список L2
Главная программа
    Вызов сдвига для L1 (вправо)
     Вызов сдвига для L2 (влево)
   Вывод результатов
ТЕСТ НА КОРРЕКТНОСТЬ
cpp
Copy
Download
#include <iostream>
#include <list>
#include <algorithm>
#include <iterator>
#include <cassert>

void testCyclicRotate() {
    std::cout << "=== ТЕСТИРОВАНИЕ CYCLIC ROTATE ===" << std::endl;
    
    
    std::list<int> test1 = {1,2,3,4,5,6,7,8,9,10};
    cyclicRotate(test1, 3, true);
    std::list<int> expected1 = {8,9,10,1,2,3,4,5,6,7};
    assert(test1 == expected1);
    std::cout << "Тест 1 (правый сдвиг): ПРОЙДЕН" << std::endl;
    
    
    std::list<int> test2 = {11,12,13,14,15,16,17,18,19,20};
    cyclicRotate(test2, 3, false);
    std::list<int> expected2 = {14,15,16,17,18,19,20,11,12,13};
    assert(test2 == expected2);
    std::cout << "Тест 2 (левый сдвиг): ПРОЙДЕН" << std::endl;
    
    
    std::list<int> test3 = {1,2,3,4,5};
    cyclicRotate(test3, 7, true); // 7 % 5 = 2
    std::list<int> expected3 = {4,5,1,2,3};
    assert(test3 == expected3);
    std::cout << "Тест 3 (K > size): ПРОЙДЕН" << std::endl;
    
    
    std::list<int> test4 = {1,2,3,4,5};
    cyclicRotate(test4, 0, true);
    std::list<int> expected4 = {1,2,3,4,5};
    assert(test4 == expected4);
    std::cout << "Тест 4 (K=0): ПРОЙДЕН" << std::endl;
    
    std::cout << "Все тесты пройдены успешно!" << std::endl;
}

int main() {
    testCyclicRotate();
    return 0;
}
КОД ЦЕЛИКОМ 
cpp
Copy
Download
#include <iostream>
#include <list>
#include <algorithm>
#include <iterator>
void cyclicRotate(std::list<int>& lst, int K, bool rotateRight) {
    int size = lst.size();
    if (size == 0) return;

    int shift = K % size;
    if (shift == 0) return; 

    auto startIt = lst.begin();
    auto middleIt = lst.begin();

    int steps = rotateRight ? (size - shift) : shift;
    std::advance(middleIt, steps);

    std::rotate(lst.begin(), middleIt, lst.end());
}

void printList(const std::string& name, const std::list<int>& lst) {
    std::cout << name << ": ";
    for (const auto& elem : lst) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::list<int> L1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::list<int> L2 = {11, 12, 13, 14, 15, 16, 17, 18, 19, 20};

    int K = 3;

    std::cout << "Исходные списки:" << std::endl;
    printList("L1", L1);
    printList("L2", L2);
    std::cout << "K = " << K << std::endl << std::endl;

    cyclicRotate(L1, K, true);  
    cyclicRotate(L2, K, false); 

    std::cout << "После циклического сдвига:" << std::endl;
    printList("L1 (сдвиг вправо)", L1);
    printList("L2 (сдвиг влево)", L2);

    return 0;
}
Задание 7. 
Дан вектор V, содержащий не менее 3 элементов. Определить значения трех конечных элементов вектора после того, как вектор будет отсортирован (по возрастанию) и вывести их в порядке убывания. Использовать один вызов алгоритма partial_sort с параметром — функциональным объектом greater и алгоритм copy для вывода требуемых элементов. 
АЛГОРИТМ РЕШЕНИЯ
1.	Сортировка последних 3 элементов с помощью partial_sort с компаратором greater<int>()
2.	Выбор последних 3 элементов отсортированного вектора
3.	Вывод в порядке убывания с использованием copy и ostream_iterator
Пример для V = {5, 2, 8, 1, 9, 3, 7}:
•	После сортировки: {1, 2, 3, 5, 7, 8, 9}
•	Три конечных элемента: 7, 8, 9
•	Вывод в порядке убывания: 9 8 7
СТРУКТУРА КОДА
text
Copy
Download
program/
Инициализация вектора V
Сортировка последних 3 элементов по убыванию
partial_sort с greater<int>
Выбор трех конечных элементов
Вывод результатов
 copy с ostream_iterator
ТЕСТ НА КОРРЕКТНОСТЬ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <algorithm>
#include <cassert>

void testThreeLargest() {
    std::cout << "=== ТЕСТИРОВАНИЕ THREE LARGEST ===" << std::endl;
    
    std::vector<int> test1 = {5, 2, 8, 1, 9, 3, 7};
    std::partial_sort(test1.end() - 3, test1.end(), test1.end(), std::greater<int>());
    std::vector<int> result1(test1.end() - 3, test1.end());
    assert(result1[0] == 9 && result1[1] == 8 && result1[2] == 7);
    std::cout << "Тест 1: ПРОЙДЕН" << std::endl;
    
    std::vector<int> test2 = {1, 2, 3};
    std::partial_sort(test2.end() - 3, test2.end(), test2.end(), std::greater<int>());
    std::vector<int> result2(test2.end() - 3, test2.end());
    assert(result2[0] == 3 && result2[1] == 2 && result2[2] == 1);
    std::cout << "Тест 2: ПРОЙДЕН" << std::endl;
    
    std::vector<int> test3 = {10, 20, 30, 40};
    std::partial_sort(test3.end() - 3, test3.end(), test3.end(), std::greater<int>());
    std::vector<int> result3(test3.end() - 3, test3.end());
    assert(result3[0] == 40 && result3[1] == 30 && result3[2] == 20);
    std::cout << "Тест 3: ПРОЙДЕН" << std::endl;
    
    std::cout << "Все тесты пройдены успешно!" << std::endl;
}
КОД ЦЕЛИКОМ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>

int main() {
    std::vector<int> V = {5, 2, 8, 1, 9, 3, 7};
    
    std::partial_sort(V.end() - 3, V.end(), V.end(), std::greater<int>());
    
    std::cout << "Три наибольших элемента в порядке убывания: ";
    std::copy(V.end() - 3, V.end(), std::ostream_iterator<int>(std::cout, " "));
    std::cout << std::endl;
    
    return 0;
}
Задание 8. 
Дан список L. Получить вектор V вещественных чисел, содержащий значения среднего арифметического для всех пар соседних элементов исходного списка (количество элементов вектора V должно быть на 1 меньше количества элементов списка L). Например, для исходного списка 1, 3, 4, 6 полученный вектор должен содержать значения 2.0, 3.5, 5.0. Использовать алгоритм adjacent_difference с итератором вставки и функциональным объектом, а также функцию-член erase для вектора V. 
АЛГОРИТМ РЕШЕНИЯ
1.	Итерация по парам соседних элементов списка L
2.	Вычисление среднего арифметического для каждой пары (a + b) / 2.0
3.	Сохранение результатов в вектор V
4.	Количество элементов в V = количество элементов в L - 1
Пример для L = {1, 3, 4, 6}:
•	Пары: (1,3) → (1+3)/2.0 = 2.0
•	(3,4) → (3+4)/2.0 = 3.5
•	(4,6) → (4+6)/2.0 = 5.0
•	Результат: V = {2.0, 3.5, 5.0}
СТРУКТУРА КОДА
text
Copy
Download
program/
Инициализация списка L
Создание пустого вектора V
Обработка пар соседних элементов
Цикл по итераторам списка
Вычисление средних значений
Вывод результатов
ТЕСТ НА КОРРЕКТНОСТЬ
cpp
Copy
Download
#include <iostream>
#include <list>
#include <vector>
#include <algorithm>
#include <cassert>

void testAdjacentAverages() {
    std::cout << "=== ТЕСТИРОВАНИЕ ADJACENT AVERAGES ===" << std::endl;
    
    std::list<int> test1 = {1, 3, 4, 6};
    std::vector<double> V1;
    auto it1 = test1.begin();
    auto next_it1 = std::next(it1);
    for (; next_it1 != test1.end(); ++it1, ++next_it1) {
        V1.push_back((*it1 + *next_it1) / 2.0);
    }
    assert(V1.size() == 3);
    assert(V1[0] == 2.0 && V1[1] == 3.5 && V1[2] == 5.0);
    std::cout << "Тест 1: ПРОЙДЕН" << std::endl;
    
    std::list<int> test2 = {10, 20};
    std::vector<double> V2;
    auto it2 = test2.begin();
    auto next_it2 = std::next(it2);
    for (; next_it2 != test2.end(); ++it2, ++next_it2) {
        V2.push_back((*it2 + *next_it2) / 2.0);
    }
    assert(V2.size() == 1);
    assert(V2[0] == 15.0);
    std::cout << "Тест 2: ПРОЙДЕН" << std::endl;
    
    std::list<int> test3 = {5, 5, 5, 5};
    std::vector<double> V3;
    auto it3 = test3.begin();
    auto next_it3 = std::next(it3);
    for (; next_it3 != test3.end(); ++it3, ++next_it3) {
        V3.push_back((*it3 + *next_it3) / 2.0);
    }
    assert(V3.size() == 3);
    assert(V3[0] == 5.0 && V3[1] == 5.0 && V3[2] == 5.0);
    std::cout << "Тест 3: ПРОЙДЕН" << std::endl;
    
    std::cout << "Все тесты пройдены успешно!" << std::endl;
}
КОД ЦЕЛИКОМ
cpp
Copy
Download
#include <iostream>
#include <list>
#include <vector>

int main() {
    std::list<int> L = {1, 3, 4, 6};
    
    std::vector<double> V;
    
    auto it = L.begin();
    auto next_it = std::next(it);
    for (; next_it != L.end(); ++it, ++next_it) {
        V.push_back((*it + *next_it) / 2.0);
    }

    for (double val : V) {
        std::cout << val << " ";
    }
    std::cout << std::endl;

    return 0;
}
Задание 9. 
Дан вектор V0, целое число N (> 0) и набор векторов V1, …, VN. Известно, что размер вектора V0 не превосходит размера любого из векторов V1, …, VN. Найти количество векторов VI, I = 1, …, N, в которых содержатся все элементы вектора V0 (без учета их повторений). Использовать алгоритм includes, применяя его в цикле к двум множествам, одно из которых создано на основе вектора V0, а другое на очередной итерации содержит элементы очередного из векторов VI, I = 1, …, N. 
АЛГОРИТМ РЕШЕНИЯ
1.	Сортировка вектора V0 для подготовки к использованию алгоритма includes
2.	Итерация по всем векторам V1, ..., VN
3.	Сортировка каждого вектора Vi перед проверкой
4.	Применение алгоритма includes для проверки содержания всех элементов V0 в Vi
5.	Подсчет количества векторов, удовлетворяющих условию
Пример для V0 = {2, 4}, V1 = {1,2,3,4,5}, V2 = {2,4,6,8}, V3 = {2,4}:
•	V1 после сортировки: {1,2,3,4,5} → includes(V1, V0) = true
•	V2 после сортировки: {2,4,6,8} → includes(V2, V0) = true
•	V3 после сортировки: {2,4} → includes(V3, V0) = true
•	Результат: count = 3
СТРУКТУРА КОДА
text
Copy
Download
program/
Инициализация V0 и набора векторов
Сортировка V0 
Цикл по всем векторам Vi
Сортировка текущего вектора Vi
Проверка includes(Vi, V0)
Увеличение счетчика при успехе
Вывод результатаТЕСТ НА КОРРЕКТНОСТЬ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <algorithm>
#include <cassert>

void testIncludesCount() {
    std::cout << "=== ТЕСТИРОВАНИЕ INCLUDES COUNT ===" << std::endl;
    
    std::vector<int> V0 = {2, 4};
    std::vector<std::vector<int>> vectors = {
        {1, 2, 3, 4, 5},
        {2, 4, 6, 8},
        {2, 4},
        {1, 3, 5},
        {4, 2, 1}
    };
    
    std::vector<int> V0_sorted = V0;
    std::sort(V0_sorted.begin(), V0_sorted.end());

    int count = 0;
    for (const auto& vec : vectors) {
        std::vector<int> sorted_vec = vec;
        std::sort(sorted_vec.begin(), sorted_vec.end());
        if (std::includes(sorted_vec.begin(), sorted_vec.end(),
                         V0_sorted.begin(), V0_sorted.end())) {
            ++count;
        }
    }
    
    assert(count == 4);
    std::cout << "Тест 1: ПРОЙДЕН" << std::endl;
    
    std::vector<int> V0_2 = {1, 3};
    std::vector<std::vector<int>> vectors2 = {
        {1, 2, 3},
        {1, 3, 5},
        {2, 4, 6}
    };
    
    std::sort(V0_2.begin(), V0_2.end());
    
    int count2 = 0;
    for (const auto& vec : vectors2) {
        std::vector<int> sorted_vec = vec;
        std::sort(sorted_vec.begin(), sorted_vec.end());
        if (std::includes(sorted_vec.begin(), sorted_vec.end(),
                         V0_2.begin(), V0_2.end())) {
            ++count2;
        }
    }
    
    assert(count2 == 2);
    std::cout << "Тест 2: ПРОЙДЕН" << std::endl;
    
    std::cout << "Все тесты пройдены успешно!" << std::endl;
}
КОД ЦЕЛИКОМ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> V0 = {2, 4};
    int N = 3;
    
    std::vector<std::vector<int>> V_vectors = {
        {1, 2, 3, 4, 5},
        {2, 4, 6, 8},
        {2, 4}
    };

    std::vector<int> V0_sorted = V0;
    std::sort(V0_sorted.begin(), V0_sorted.end());

    int count = 0;

    for (int i = 0; i < N; ++i) {
        std::vector<int> Vi = V_vectors[i];
        
        std::sort(Vi.begin(), Vi.end());

        if (std::includes(Vi.begin(), Vi.end(),
                          V0_sorted.begin(), V0_sorted.end())) {
            ++count;
        }
    }

    std::cout << "Количество векторов, содержащих все элементы V0: " << count << std::endl;

    return 0;
}
Задание 10. 
Дан вектор V, элементами которого являются английские слова, набранные заглавными буквами. Определить суммарную длину слов, начинающихся с одной и той же буквы, и вывести все различные буквы, с которых начинаются элементы вектора V, вместе с суммарной длиной этих элементов (в алфавитном порядке букв); длину выводить сразу после соответствующей буквы. Использовать вспомогательное отображение M, ключами которого являются начальные буквы элементов вектора V, а значениями — суммарная длина этих элементов. При заполнении отображения M не использовать условные конструкции (достаточно операций индексирования [], инкремента и функции-члена size для строк). Элементы вектора V (при заполнении отображения M) и элементы отображения M (при выводе полученных результатов) перебирать в цикле с параметром-итератором соответствующего контейнера. 
АЛГОРИТМ РЕШЕНИЯ
1.	Итерация по всем словам в векторе V
2.	Извлечение первой буквы каждого слова
3.	Обновление отображения M с использованием операции индексирования []
4.	Автоматическое создание записей при первом обращении к ключу
5.	Вывод результатов в алфавитном порядке (автоматически обеспечивается map)
Пример для V = {"APPLE", "ARM", "BANANA", "BALL", "CAT", "CAR"}:
•	'A': APPLE(5) + ARM(3) = 8
•	'B': BANANA(6) + BALL(4) = 10
•	'C': CAT(3) + CAR(3) = 6
•	Результат: A8 B10 C6
СТРУКТУРА КОДА
text
Copy
Download
program/
 Инициализация вектора слов V
Создание пустого отображения M
Заполнение отображения Цикл по словам с добавлением длин
Вывод результатов
Цикл по отображению в алфавитном порядке
ТЕСТ НА КОРРЕКТНОСТЬ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <map>
#include <string>
#include <cassert>

void testWordLengths() {
    std::cout << "=== ТЕСТИРОВАНИЕ WORD LENGTHS ===" << std::endl;
    
    std::vector<std::string> test1 = {"APPLE", "ARM", "BANANA", "BALL", "CAT", "CAR"};
    std::map<char, size_t> M1;
    
    for (auto it = test1.begin(); it != test1.end(); ++it) {
        char first_char = (*it)[0];
        M1[first_char] += it->size();
    }
    
    assert(M1['A'] == 8);
    assert(M1['B'] == 10);
    assert(M1['C'] == 6);
    std::cout << "Тест 1: ПРОЙДЕН" << std::endl;
    
    std::vector<std::string> test2 = {"DOG", "DOOR", "EAGLE"};
    std::map<char, size_t> M2;
    
    for (auto it = test2.begin(); it != test2.end(); ++it) {
        char first_char = (*it)[0];
        M2[first_char] += it->size();
    }
    
    assert(M2['D'] == 7);
    assert(M2['E'] == 5);
    std::cout << "Тест 2: ПРОЙДЕН" << std::endl;
    
    std::vector<std::string> test3 = {"ZOO"};
    std::map<char, size_t> M3;
    
    for (auto it = test3.begin(); it != test3.end(); ++it) {
        char first_char = (*it)[0];
        M3[first_char] += it->size();
    }
    
    assert(M3['Z'] == 3);
    std::cout << "Тест 3: ПРОЙДЕН" << std::endl;
    
    std::cout << "Все тесты пройдены успешно!" << std::endl;
}
КОД ЦЕЛИКОМ
cpp
Copy
Download
#include <iostream>
#include <vector>
#include <map>
#include <string>

int main() {
    std::vector<std::string> V = {"APPLE", "ARM", "BANANA", "BALL", "CAT", "CAR"};

    std::map<char, size_t> M;

    for (auto it = V.begin(); it != V.end(); ++it) {
        char first_char = (*it)[0];
        M[first_char] += it->size();
    }

    for (auto it = M.begin(); it != M.end(); ++it) {
        std::cout << it->first << it->second << std::endl;
    }

    return 0;
}

