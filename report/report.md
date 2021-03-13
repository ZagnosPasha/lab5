---
# Front matter
lang: ru-RU
title: "Лабораторная работа №5"
subtitle: "Модель хищник-жертва"
author: "Алли Мохамед Заян"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Ознакомление с простейшей моделью взаимодействия двух видов типа «хищник — жертва» - моделью Лотки-Вольтерры  и ее построение с помощью языка программирования Modelica. 

# Задание

1. Построить график зависимости численности хищников от численности жертв.
2. Построить графики изменения численности хищников и численности жертв.
3. Найти стационарное состояние системы.

# Выполнение лабораторной работы

Уравнение модели "хищник-жертва" имеет следующий вид:
	$$ 
                \begin{cases}
                    \frac{dx}{dt} = -0.47x(t)+0.021x(t)y(t)
                    \\
                    \frac{dy}{dt} = 0.57y(t)-0.044x(t)y(t)
                 \end{cases}
        $$
Начальные условия: x_0 = 6 и y_0 = 19.
1. Ниже приведен код программы, реализованный на языке программирования Modelica (рис 1. -@fig:001)  

![Код программы для решения задачи](image/1.png){ #fig:001 width=70% }

Также ниже приведен график зависимости численности популяции хищников от численности популяции жертв. (рис 2. -@fig:001)  

![График зависимости численности хищников от численности жертв](image/2.png){ #fig:001 width=70% }

2. Построим графики изменения численности популяции хищников и численности популяции жертв с течением времени (рис 3. -@fig:001)  

![Графики изменения численности хищников и численности жертв с течением времени](image/3.png){ #fig:001 width=70% }

3. Для того, чтобы найти стационарное состояние системы, необходимо приравнять производные каждой из функций x и y к нулю и выразить значения y и x соответственно.  

Получим следующие значения:
$$ x_0 = \frac{b}{d} = \frac{0.57}{0.044} \approx 12.95  $$
$$ y_0 = \frac{a}{c} = \frac{0.47}{0.021} \approx 22.38  $$
При стационарном состоянии значения числа жертв и хищников не меняется во времени. (рис 4. -@fig:001)  

![Стационарное состояние системы](image/4.png){ #fig:001 width=70% }

# Код программы

Приведу полный код программы (Modelica):    
model Predator  
parameter Real a = 0.47; // коэффициент естественной смертности хищников  
parameter Real b = 0.57; // коэффициент естественного прироста жертв  
parameter Real c = 0.021; // коэффициент увеличения числа хищников  
parameter Real d = 0.044; // коэффициент смертности жертв  
//parameter Real x0 = 12.0;// начальная популяция хищников  
//parameter Real y0 = 37.0;// начальная популяция жертв  
parameter Real x0 = 0.57/0.044;// стационарое состояние хищников (b/d)  
parameter Real y0 = 0.47/0.021;// стационарое состояние жертв (a/c)  
Real x(start=x0);// популяция хищников  
Real y(start=y0);// популяция жертв  
equation  
der(x) = -a*x + c*x*y;  
der(y) = b*y - d*x*y;  
end Predator;  

# Выводы

Ознакомился с простейшей моделью взаимодействия двух видов типа «хищник — жертва», построив для нее графики и найдя стационарное состояние системы. 
