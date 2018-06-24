# Определение координат отверстий под коннекторы на материнских платах с помощью компьютерного зрения

Сейчас на многих заводах по производству материнских плат габаритные компоненты размещаются вручную. В их число входят разъемы для модуля памяти, разъемы питания, разъемы ввода/вывода: USB, HDMI, Audio-коннекторы и другие. Чтобы освободить людей от монотонного физического труда и повысить скорость и качество выполняемой работы, необходимо использование манипуляционного робота с системой машинного зрения. 

Необходимо с помощью камеры, установленной на фланце робота, получить изображение рабочей зоны, в которой находится материнская плата, произвести обработку и анализ этого изображения, и определить координаты точки в системе координат рабочей зоны, к которой привязан робот. Далее координаты этой точки передаются в систему управления манипуляционного робота, который выполняет операцию вставки коннектора.

Предварительно производится калибровка камеры - определяются параметры внутренней матрицы камеры и коэффициенты дисторсии, которые используются для получения скорректированного изображения. На скорректированном изображении определяются границы с помощью алгоритма Canny и контур материнской платы. Внутри этого контура происходит поиск областей с отверстиями под коннекторы различных типов, используются алгоритмы SURF и FLANN based Matcher, определяются координаты геометрических центров этих областей в системе координат изображения. Необходимо посчитать эти координаты в системе координат рабочей зоны.

В рабочей зоне находятся 4 реперные точки, имеющие форму окружности, координаты которых в системе координат рабочей зоны известны. С помощью Hough Transform на изображении определяются окружности, которые соответствуют реперным точкам, в результате чего координаты реперных точек на изображении становятся известны. Так как координаты реперных точек в двух системах координат и параметры внутренней матрицы камеры известны, то для данного изображения определяются параметры внешней матрицы камеры. Используя внутреннюю и внешнюю матрицы камеры, а также координаты точек центров областей на изображении, считаются координаты этих точек в системе координат рабочей зоны, эти координаты передаются в систему управления робота.
