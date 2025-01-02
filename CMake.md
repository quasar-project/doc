## CMake
#### Опции
> [!WARNING]
> Не рекомендуется использовать CMake для конфигурации напрямую. Предпочтительнее конфигурировать процесс сборки библиотеки с помощью 
> пакетного менеджера `conan` (см. далее).

CMake-файл предоставляет следующие опции для конфигурации процесса сборки библиотеки:
- `QUASAR_TESTS` - управляет сборкой тестов. По умолчанию - **OFF**.
- `QUASAR_PYTHON` - управляет сборкой биндингов для Python. По умолчанию - **ON**.
- `QUASAR_CUDA` - используется ли NVidia CUDA. По умолчанию - **ON**.

Опции можно передавать в командную строку при запуске сборки при помощи параметров `cmake`:
```shell
cmake -S . -B target -DQUASAR_TESTS=ON -DQUASAR_PYTHON=ON -DQUASAR_CUDA=ON
```

#### Команды
> [!TIP]
> При сборке библиотеки напрямую через CMake без использования `conan`, не забывайте, что CMake собирает библиотеку в режиме **Debug** по умолчанию. Чтобы собрать библиотеку в режиме **Release**, необходимо использовать опцию `-DCMAKE_BUILD_TYPE=Release`.

###### Конфигурация
```shell
cmake -S . -B target -DQUASAR_CUDA=ON -DCMAKE_BUILD_TYPE=Release
```

###### Сборка
```shell
cmake --build target --config Release --parallel
```

Для сборки через Conan:
```shell
cmake --preset "conan-release" && cmake --build build/Release --parallel
```

После успешной сборки в папке `py3` автоматически появится нужный файл модуля Python.
