# Памятка по работе с проектом

## Начало работы с проектом
Для начала работы с проектом необходимо создать репозиторий по [шаблону](https://github.com/ktsstudio/backend-school-template-project). Для этого используйте кнопку "Use this template".

<img width="579" alt="image" src="https://github.com/ktsstudio/backend-school-template-project/assets/79798334/1566de18-2be5-4570-b327-fa212f909ab0">

После этого его можно локально клонировать себе на компьютер:

``` sh
git clone <ссылка на репозиторий>
```

---
## Ветки dev и main
После того как скопируете репозиторий, скорее всего, вы будете находиться в main-ветке. 

Как правило, ветка `main` (`master`) содержит в себе _production-ready_ код, т.е. именно из этой ветки проект будет катиться. Поэтому сама разработка из этой ветки обычно не ведется, туда делают merge финальных изменений.

Создадим ветку dev:
``` sh
git checkout -b dev
```

Dev — чаще всего общая тестовая ветка. От `dev-ветки` ответвляются `feature-ветки`, в которые добавляется новая функциональность, тестируется, проходит ревью и "сливается" в `dev-ветку`.

Создадим `feature`-ветку:
``` sh
git checkout -b <<название ветки>>
```

После чего создается [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

`Pull request (PR)` позволяет другим разработчикам провести ревью и оставить комментарии к написанному коду, прежде чем проверять его и делать релиз.


---
## Работа в репозитории

### Gitignore

Файл .gitignore содержит информацию о том, какие файлы не следует сохранять в удаленный репозиторий – локальные конфиги, файлы библиотек, специфичные файлы IDE или операционной системы.  

Самый простой способ составить подходящий `.gitignore` файл — воспользоваться ресурсом [gitignore.io](https://www.toptal.com/developers/gitignore/)


Обратите внимание, что в шаблоне проекта уже присутствует файл `.gitignore`. Остается убедиться, что у вас нет каких-то дополнительных файлов, которые следует туда добавить.

---
### Виртуальное окружение

#### Создание виртуального окружения

Виртуальное окружение позволяет разделять проекты, зависимости и даже версии языка.

**Пример.** Есть два проекта. Один использует библиотеку `example` версии 1, второй – версии 2. Они не могут существовать одновременно, и версии могут конфликтовать из-за каких-то других зависимостей. Поэтому мы создаем два виртуальных окружения, каждое для своего проекта. `PyCharm` может создавать их автоматически. `Python` будет видеть только библиотеки из своего виртуального окружения, что существенно облегчит сосуществование множества проектов на одном компьютере.

**Создадим:**
``` sh
python -m venv <название окружения>
```

> Принято называть окружение `env` или `venv` -– `([virtual] environment)`.

Задать версию языка для виртуального окружения, например 3.12:
```
python3.12 -m venv <название окружения>
```

> Обратите внимание, что для этого нужно чтобы эта версия была установлена в системе.


#### Активация
**Для Linux/MacOS:**
``` sh
source <название окружения>/bin/activate
```

**Для Windows:**
``` sh
<название окружения>\Scripts\activate.bat
```

---
### Зависимости
В файл `requirements.txt` принято записывать зависимости проекта – список библиотек и их версий, без которых проект не сможет запуститься. Добавляя в проект использование новой библиотеки, обязательно нужно записать ее в `requirements.txt`. При релизе зависимости устанавливаются из же этого файла.

Пример файла:
```requirements.txt
aiohttp==3.8.1
black==22.6.0
freezegun==1.2.1
pytest==7.1.2
pytest-aiohttp==1.0.4
```

Если в новой версии из библиотеки будет удалено что-то важное для проекта, то ничего не сломается, потому что мы фиксируемся на старой версии. В дальнейшем мы можем вручную обновить версию и сразу проследить, что при обновлении все работает как нужно. Либо что-то починить, если сломалось.

Установить все необходимые библиотеки можно при помощи команды…
```sh
pip install <библиотека>
```

…либо:
```sh
pip install -r requirements.txt
```

Лучше всего ставить библиотеки в виртуальное окружение.

---
### Ruff
[Библиотека](https://docs.astral.sh/ruff/) для автоматического форматирования кода и проверки его на ошибки. Рекомендуется использовать, чтобы код был читаемым и соответствовал `pep-8`. Для применения потребуется поставить библиотеку в виртуальное окружение.

**Отформатировать код:**
```sh
ruff format  
```

**Проверить код**
```sh
ruff check --fix  
```

В файле `pyproject.toml` можно сконфигурировать библиотеку. 

Например:
```toml
[tool.ruff]
line-length = 80
indent-width = 4
target-version = "py312"
```

> Обратите внимание, что в `pyproject.toml` для вас уже добавлена рекомендуемая конфигурация. 
> По договоренности с вашим ментором конфигурацию можно отредактировать.