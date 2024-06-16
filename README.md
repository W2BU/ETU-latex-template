# Шаблон оформления студенческих работ СПбГЭТУ "ЛЭТИ"

LaTex шаблон для оформления выпускной квалификационной работы, курсовых или лабораторных работ в соответствии с нормоконтролем СПбГЭТУ "ЛЭТИ" 2024.

# Особенности

* XeLaTex
* 14pt Times New Roman, полуторный интервал, красная строка 1.25 см
* Вставка листингов при помощи пакетов listings или minted
* Макросы для ссылок на изображения, таблицы, листинги
* Автоматическая нумерация приложений
* Библиография BibLaTex + Biber
* Оформление библиографии в соответствии с ГОСТ 2008
* Нумерация изображений, таблиц, листингов с учетом номера главы
* Гиперссылки на оглавление, приложения, изображения, цитаты, формулы, таблицы, листинги.


# Структура проекта

```
vkr
 ┣ chapters
 ┃ ┣ chapter1.tex
 ┃ ┣ chapter2.tex
 ┃ ┣ chapter3.tex
 ┃ ┗ chapter4.tex
 ┣ img
 ┃ ┗ app-pic.png
 ┣ listing 
 ┃ ┗ code_sample.py
 ┣ setup
 ┃ ┣ FiraCode-Regular.ttf
 ┃ ┣ format.tex
 ┃ ┣ listings.tex
 ┃ ┣ macros.tex
 ┃ ┗ packages.tex
 ┣ title
 ┃ ┣ vkr_title.pdf
 ┃ ┗ lab_title.tex
 ┣ annotation.tex
 ┣ appendix.tex
 ┣ bib.tex
 ┣ chapters.tex
 ┣ conclusion.tex
 ┣ introduction.tex
 ┣ lab_content.tex
 ┣ main.tex
 ┣ refs.bib
 ┣ main.tex
 ┗ summary.bib
```

В папке chapters собраны файлы с содержанием глав. Сами же главы включаются в проект в файле chapters.tex.

Папка img содержит файлы изображений.

Папка listing содержит файлы листингов кода с соответствующими расширениями.

В папке title собраны титульный лист для ВКР в формате PDF &ndash; vkr_title.pdf и титульный лист для лабораторной работы в формате tex &ndash; lab_title.tex

В папке setup расположены файлы настроек проекта:
* FiraCode-Regular.ttf &ndash; шрифти для листингов minted
* format.tex &ndash; в файле задаются правила форматирования из пакетов
* macros.tex &ndash; описание пользовательских комманд
* packages.tex &ndash; перечень подключенных пакетов


Далее перечислены файлы разделов ВКР:
* annotation.tex &ndash; аннотация(реферат)
* appendix.tex &ndash; приложения к работе
* bib.tex &ndash; раздел библиографии
* chapters.tex &ndash; содержание работы/включенные главы
* conclusion.tex &ndash; заключение к работе
* introduction.tex &ndash; введение к работе
* main.tex &ndash; основной файл проекта
* summary.tex &ndash; содержание работы (Table of Content)

Содержание лабораторной работы, ради удобства вынесено в отдельный файл lab_content.tex

# Сборка проекта

Автор производил сборку при помощи расширения LaTeX Workshop в среде VS Code с установленным texlive. 

Предлагаемая последовательность:

XeLaTeX -> biber -> XeLaTeX -> XeLaTeX

Рецепт сборки для VS Code:

```

     "latex-workshop.latex.recipes": 
        {
            "name": "xelatex -> biber -> xelatex*2",
            "tools": [
                "xelatex",
                "biber",
                "xelatex",
                "xelatex"
            ]
        }

    "latex-workshop.latex.tools":
        {
            "args": [
                "--shell-escape",
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "command": "xelatex",
            "env": {},
            "name": "xelatex"
        },
        {
            "args": [
                "%DOCFILE%"
            ],
            "command": "biber",
            "env": {},
            "name": "biber"
        },
```
**Для работы minted необходим аргумент --shell-escape и интерпретатор языка Python с установленным пакетом *pygmentize***