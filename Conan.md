## Conan
Conan - это пакетный менеджер для C/C++. В этом проекте он используется для платформонезависимого разрешения зависимостей (например, для установки *pybind11*).

#### Предварительная конфигурация системы
Необходимо установить все необходимые пакеты pip для сборки библиотеки. Для этого в корне проекта выполняем команду 
```shell
pip install -r requirements.txt`
```

Затем конфигурируем профиль сборки по умолчанию:
```shell
conan profile detect --force &&
sed -i /compiler.cppstd/c\compiler.cppstd=gnu17 ~/.conan2/profiles/default
```
> Настоятельно рекомендуется использовать утилиту `ninja` для компиляции проекта, так как она обеспечивает ускорение параллельной сборки в 1.5-2 раза.
> 
> Чтобы `conan` автоматически использовал `ninja` для сборки проекта, нужно добавить следующую строчку в конец файла `~/.conan/profiles/default`:
> 
> ```ignore
> [conf]
> tools.cmake.cmaketoolchain:generator=Ninja
> ```
> 
> Установить `ninja` можно вручную с помощью команды: 
> ```shell
> sudo apt install ninja-build
> ```

#### Опции
Файл конфигурации `conanfile.py` содержит следующие опции:
- `shared` - управляет сборкой библиотеки в статическом или динамическом режиме. По умолчанию - **True** (динамическая библиотека).
- `test` - управляет сборкой тестов. По умолчанию - **False**.
- `cuda` - используется ли NVidia CUDA. По умолчанию - **True**.
- `python_bindings` - управляет сборкой биндингов для Python. По умолчанию - **True**.
- `native_pybind` - отключает зависимость от встроенного *pybind11* и полагается на системный. По умолчанию - **False**.

Опции можно передавать при помощи флага `-o "quasar/*:ИМЯ_ОПЦИИ=ЗНАЧЕНИЕ"`, например:
```shell
conan install . -o "quasar/*:shared=True" -o "quasar/*:test=True" -o "quasar/*:cuda=True" -o "quasar/*:python_bindings=True"
```

#### Команды
###### Конфигурация
```shell
conan install . -o "quasar/*:shared=True" -o "quasar/*:test=True" -o "quasar/*:cuda=True" -o "quasar/*:python_bindings=True"
```

###### Сборка
```shell
conan build . -b "missing" -o "quasar/*:shared=True" -o "quasar/*:test=True" -o "quasar/*:cuda=True" -o "quasar/*:python_bindings=True"
```

По умолчанию будет собрана **релизная** версия. Необходимо указать опцию `-s build_type=Debug`, чтобы собрать версию для отладки.