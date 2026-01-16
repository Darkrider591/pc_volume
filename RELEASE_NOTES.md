# v2.2 STABLE
1. Disabled some unnecessary settings
2. Visual interface changes

# v2.1 STABLE
1. Visualization of points and surfaces
2. Changing the plot view: Isometric, Top View, Front View
3. Saving screenshots
4. Color scales by height
5. Volumes and areas are now displayed
6. Compatibility with Tkinter + PyVista

# v2.0 STABLE/MAJOR Update
1. Switched from matplotlib to pyvista for improved performance
2. Translated into English due to pyvista's lack of Cyrillic support

# v1.9 DEMO/MAJOR Update
1. Added support for .las files
2. Added support for .csv/.xyz files
3. Added a bottom surface interpolation method
4. Visualization changes - Height differences are shown in color
5. Added saving results to Excel

# v1.8 STABLE
1. Added color gradient and rotation animation.

# v1.7 STABLE/MAJOR Update
1. Created a desktop window with win buttons for loading source data and visualizing results.

# v1.6 STABLE
1. Added additional parameters to the results graph: surface areas in 2D and 3D.

# v1.5 STABLE
1. Added 3D graph output with the upper and lower surfaces displayed.

# v1.4 STABLE
1. Added a function for displaying results in a separate window to ensure correct operation when working with .exe files.

# v1.3 STABLE
1. Added a function for importing surface files from a local drive.

# v1.2 STABLE
1. Added a function for calculating possible surface intersections, i.e., a CUT/FILL calculation.

# 1.1 STABLE
1. Changed the area calculation logic: A new compute_area function has been used, which sums the areas of all triangles in a triangulation using Heron's formula.

# 1.0 STABLE
1. Loading Data:
The load_points() function loads data from text files containing point coordinates in the (X, Y, Z) format and performs a number of checks:

The file exists and is readable.
The data is in the correct format (at least three columns).
The number of rows is greater than zero.
The data is processed using the NumPy library, which allows for efficient manipulation of multidimensional arrays.

2. Creating a Spatial Tree Structure (KD-trees):
KD-trees are used to speed up the search for the closest point between surfaces. This data structure allows for quickly finding the closest point in a large set of coordinates.

When processing each vertex of the main point set, the algorithm searches for the closest vertex on the opposite surface to determine the height and volume of each partition element.

3. Surface Triangulation:
The SciPy library provides tools for triangulating (Delaunay triangulation) a set of points. It triangulates the plane to minimize the number of narrow corners and optimize the distribution of mesh elements.

This is an important step before further calculating volumes and areas, as triangulation allows each surface region to be processed separately.

4. Determining Surface Area:
The algorithm determines surface area by calculating the sum of the areas of all triangles obtained by triangulation. However, the source code you provided uses an incorrect area determination method—instead of correctly calculating the area of ​​a polyline, it uses the area of ​​the boundary of a convex polygon (the ConvexHull.area method), which will lead to an incorrect result.

5. Selecting a Base Surface:
The program selects one of the surfaces as the basis for volume calculations based on its area. The surface with the smaller area is considered the base ("bounding") surface, which helps avoid potential errors in the subsequent integration process.

6. Volume calculation:
The basic principle of the calculation is as follows:

Each point on one surface is compared with the nearest point on the other surface.
Then, for each triangle of the main surface, the average height difference is determined and multiplied by the area of ​​that triangle.
The resulting volumes of the individual areas are added together, forming the final total volume of the space between the surfaces.

The volume calculation formula is as follows:
Vtotal=i=1∑N(3Ai+Bi+Ci−Z)⋅Area(Ti),

_______________________________________________________________________________________________


# v2.2 STABLE
1. Отключены некоторые ненужные настройки
2. Визуальные изменения интерфейса

# v2.1 STABLE
1. Визуализация точек и поверхностей
2. Изменение ракурса: Isometric, Top View, Front View
3. Сохранение скриншотов
4. Цветовые шкалы по высоте
5. Отображаются объёмы и площади
6. Совместимость с Tkinter + PyVista

# v2.0 STABLE/MAJOR Update 
1. Переход с matplotlib на pyvista для повышеняи производительности
2. Переведено на английский, изза отсутствия поддержки pyvista кирилицы

# v1.9 DEMO/MAJOR Update 
1. Добавлена поддержка las файлов
2. Добавлена поддержка .csv/.xyz
3. Добавлен метод интерполяции нижней поверхности
4. Изменена визуализаци - Цветом показана разница высот
5. Добавлен осохранение результатов в Excel

# v1.8 STABLE
1. Добавлен градиент цветов и анимации вращения 

# v1.7 STABLE/MAJOR Update 
1. Создано десктоп окно с кнопками win для загрузки исходных данных и визуализации результатов

# v1.6 STABLE
1. Добавлен вывод в результатов на график дополнительных параметров: плозади поверхностей в 2D и 3D

# v1.5 STABLE
1. Добавлен вывод графика в 3d с отображением верхней и нижней поверхности

# v1.4 STABLE
1. Добавлена функция вывода результата в отдельном окне для корректной работе при работе exe файлов

# v1.3 STABLE
1. Добавлена функция импорта файлов поверхностей с локального диска

# v1.2 STABLE
1. Добавлена функция расчет с учетом возможных пересечений поверхностей, т.е. расчет CUT/FILL

# 1.1 STABLE
1. Изменена логика расчета площадей: Использована новая функция compute_area, которая суммирует площади всех треугольников триангуляции, используя формулу Герона.

# 1.0 STABLE
1. Загрузка данных:
Функция load_points() загружает данные из текстовых файлов, содержащих координаты точек в формате (X, Y, Z) и проводит ряд проверок:

Файл существует и доступен для чтения.
Данные имеют правильный формат (не менее трёх колонок).
Количество строк больше нуля.
Данные обрабатываются с использованием библиотеки NumPy, которая позволяет эффективно манипулировать многомерными массивами.

2. Создание структуры пространственных деревьев (KD-trees):
Для ускорения поиска ближайшей точки между поверхностями используются KD-деревья. Это структура данных, позволяющая быстро находить ближайшую точку в большом наборе координат.

При обработке каждой вершины основного множества точек, алгоритм ищет ближайшую вершину на противоположной поверхности, чтобы определить высоту и объем каждого элемента разбиения.

3. Триангуляция поверхностей:
Библиотека SciPy предоставляет инструменты для триангуляции (Delaunay-триангуляция) набора точек. Она разбивает плоскость на треугольники таким образом, чтобы минимизировать количество узких углов и оптимизировать распределение элементов сетки.

Это важный этап перед дальнейшим вычислением объёмов и площадей, поскольку триангуляция даёт возможность обрабатывать каждую отдельную область поверхности отдельно.

4. Определение площади поверхности:
Алгоритм определяет площадь поверхности путём вычисления суммы площадей всех треугольников, полученных в результате триангуляции. Однако в представленном вами исходнике используется некорректная методика определения площади — вместо правильного расчёта площади полилинии используется площадь границы выпуклого многоугольника (метод ConvexHull.area), что приведёт к неправильному результату.

5. Выбор базовой поверхности:
Программа выбирает одну из поверхностей в качестве основы для расчетов объёма исходя из размера её площади. Поверхность с меньшими площадями принимается за базовую («ограничивающую»), что помогает избежать возможных ошибок в дальнейшем процессе интегрирования.

6. Подсчет объёма:
Основной принцип расчета заключается в следующем:

Каждая точка на одной поверхности сопоставляется с ближайшей точкой на другой поверхности.
Затем для каждого треугольника основной поверхности определяется средняя разница высот и умножается на площадь этого треугольника.
Полученные объёмы отдельных областей складываются вместе, формируя итоговый общий объём пространства между поверхностями.

Формула расчёта объёма выглядит следующим образом:
Vtotal=i=1∑N(3Ai+Bi+Ci−Z)⋅Area(Ti),
