# KytyPS5

[![Сборка KytyPS5 (Windows)](https://img.shields.io/github/actions/workflow/status/KytyPS5/KytyPS5/build.yml?branch=main&event=push&label=Build%20KytyPS5%20%28Windows%29)](https://github.com/KytyPS5/KytyPS5/actions/workflows/build.yml)
[![Сборка KytyPS5 (Linux)](https://img.shields.io/github/actions/workflow/status/KytyPS5/KytyPS5/build.yml?branch=main&event=push&label=Build%20KytyPS5%20%28Linux%29)](https://github.com/KytyPS5/KytyPS5/actions/workflows/build.yml)
[![Сборка KytyPS5 (macOS)](https://img.shields.io/github/actions/workflow/status/KytyPS5/KytyPS5/build.yml?branch=main&event=push&label=Build%20KytyPS5%20%28macOS%29)](https://github.com/KytyPS5/KytyPS5/actions/workflows/build.yml)
[![Платформа](https://img.shields.io/badge/platform-Windows%20x64%20%7C%20Linux%20x64%20%7C%20macOS%20x86__64-0078D4.svg)](#system-requirements)
[![Статус](https://img.shields.io/badge/status-active%20development-orange.svg)](#current-status)
[![Лицензия](https://img.shields.io/badge/license-GPL--2.0-blue.svg)](LICENSE)

**[Еженедельные обновления](https://github.com/KytyPS5/KytyPS5/discussions/862)** — прогресс в играх, недавние исправления и текущая разработка.

**[Разработка в Discord](https://discord.gg/UNrkMqGaBg)** — разработка KytyPS5.

KytyPS5 — это бесплатный эмулятор PlayStation 5 с открытым исходным кодом, написанный на C++ для Windows и Linux, с экспериментальной поддержкой macOS. Он основан на сильно изменённой версии [Kyty](https://github.com/InoriRus/Kyty). Проект активно развивается, и поведение может значительно меняться от сборки к сборке.

> [!IMPORTANT]
> KytyPS5 не связан с Sony Interactive Entertainment или PlayStation. Проект не распространяет игры или защищённое авторским правом системное программное обеспечение. Используйте только файлы игр, полученные легально.

## Текущий статус

KytyPS5 может запускать 2D-игры и некоторые 3D-игры, включая проекты, созданные на Unreal Engine 4/5, Unity и собственных движках. Внешние низкоуровневые модули эмуляции не требуются и не планируются.

Разработка в настоящее время сосредоточена на расширении совместимости с играми и повышении надёжности запуска.

Windows и Linux — основные платформы, и они тестируются больше всего.

Поддержка macOS экспериментальная. Эмулятор собран для x86-64 и работает на Apple Silicon под Rosetta 2, а Vulkan предоставляется MoltenVK. Небольшое число игр было проверено в игровом процессе на оборудовании Apple Silicon; см. [Сборка в macOS](#сборка-в-macos).

Результаты тестирования игр сообществом доступны в [списке совместимости KytyPS5](https://kytyps5.github.io/).

## Ошибки и проблемы

Совместимость, стабильность и производительность могут различаться между версиями. Вы можете столкнуться с падениями или графическими артефактами, поэтому при сообщении о проблеме указывайте версию, которую вы тестировали.

## Скриншоты

<table align="center">
  <tr>
    <td align="center">
      <strong>Astro Bot</strong><br>
      <img src="docs/screenshots/ps5-01.png" width="300" alt="Astro Bot running in KytyPS5">
    </td>
    <td align="center">
      <strong>Dreaming Sarah</strong><br>
      <img src="docs/screenshots/ps5-03.png" width="300" alt="Dreaming Sarah running in KytyPS5">
    </td>
  </tr>
  <tr>
    <td align="center">
      <strong>Neptunia ReVerse</strong><br>
      <img src="docs/screenshots/ps5-04.png" width="300" alt="Neptunia ReVerse running in KytyPS5">
    </td>
    <td align="center">
      <strong>SILENT HILL: The Short Message</strong><br>
      <img src="docs/screenshots/ps5-05.png" width="300" alt="SILENT HILL: The Short Message running in KytyPS5">
    </td>
  </tr>
  <tr>
    <td align="center">
      <strong>Demon's Souls</strong><br>
      <img src="docs/screenshots/ps5-02.png" width="300" alt="Demon's Souls running in KytyPS5">
    </td>
    <td align="center">
      <strong>UFC 5</strong><br>
      <img src="docs/screenshots/ps5-06.png" width="300" alt="UFC 5 running in KytyPS5">
    </td>
  </tr>
</table>

<p align="center"><em>И многие другие...</em></p>

## Участие в проекте

Тестирование игр и отправка подробных отчётов об ошибках — полезные способы внести вклад. Сначала поищите существующие issues, затем используйте шаблон **Game Emulation Status Report** и прикрепите полный файл журнала.

Вклад в код должен быть целенаправленным, успешно собираться на платформах, которых он касается, и, где это возможно, включать соответствующие тесты. Windows — основная целевая платформа, поэтому изменение, затрагивающее общий код, не должно ухудшать её работу; изменения, ограниченные собственными путями кода платформы, должны собираться только там. Поскольку KytyPS5 всё ещё быстро развивается, подумайте об открытии issue перед началом крупного изменения.

### Форматирование

Настройте хук clang-format после клонирования:

Установите `pre-commit` способом, подходящим для вашей платформы:

- **Arch Linux / CachyOS:** `sudo pacman -S pre-commit`
- **Другие Linux / macOS / Windows:** `python -m pip install pre-commit`

Затем установите Git-хук:

```bash
python -m pre_commit install --install-hooks
```

Он форматирует подготовленные `.cpp`, `.h` и `.inc` файлы в `src`.

## Информация для разработчиков

Графическая архитектура PS5 основана на AMD RDNA 2. Используйте [RDNA 2 Instruction Set Architecture Reference Guide (документ 70648)](https://docs.amd.com/v/u/en-US/rdna2-shader-instruction-set-architecture) от AMD в качестве основного справочника по кодированию инструкций при работе над декодированием и рекомпиляцией шейдеров.

Важные области кодовой базы:

- [`src/graphics/shader/recompiler`](src/graphics/shader/recompiler) — декодирование инструкций, промежуточное представление, управляющий поток, отслеживание ресурсов и генерация SPIR-V
- [`src/graphics/guest_gpu`](src/graphics/guest_gpu) — форматы GPU PS5 (Prospero) и обработка команд
- [`src/graphics/host_gpu`](src/graphics/host_gpu) — бэкенд Vulkan для хоста и управление ресурсами
- [`tests`](tests) — целенаправленные регрессионные тесты памяти, шейдеров и отслеживания ресурсов

Рендерер ориентирован на Vulkan 1.3. Согласовывайте изменения шейдеров как с семантикой ISA RDNA 2, так и с правилами валидации Vulkan/SPIR-V.

## Сборка

### Системные требования

- Windows 10 версии 1803, актуальный дистрибутив Linux или macOS на Apple Silicon
- 64-битный x86-процессор (на macOS — процессор Apple Silicon с Rosetta 2)
- GPU с поддержкой Vulkan 1.3 и актуальными драйверами (на macOS Vulkan предоставляется встроенным MoltenVK)

### Требования для сборки (Windows)

- Git
- CMake 3.22.1 или новее
- Ninja
- Visual Studio 2022 или Build Tools 2022 с рабочей нагрузкой **Desktop development with C++** и компонентом **C++ Clang tools for Windows**
- Qt 6 для MSVC 2022 64-бит, включая Concurrent, Network и Widgets
- [glslang](https://github.com/KhronosGroup/glslang/releases) (`glslangValidator`) в `PATH`

Компилятор Microsoft C++ (`cl.exe`) не поддерживается; используйте `clang-cl`.

Откройте **x64 Native Tools Command Prompt for Visual Studio 2022** (или эквивалентный Developer PowerShell), перейдите в корень репозитория и инициализируйте зависимости:

```powershell
git submodule update --init --recursive
```

Настройте проект. Замените путь Qt на версию, установленную в вашей системе:

```powershell
cmake -S . -B _Build/windows -G Ninja -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=clang-cl -DCMAKE_CXX_COMPILER=clang-cl -DCMAKE_PREFIX_PATH="C:/Qt/6.x.x/msvc2022_64"
```

Соберите лаунчер и подготовьте запускаемую установку:

```powershell
cmake --build _Build/windows --target launcher
cmake --install _Build/windows --prefix _Build/windows/install
```

Готовое приложение и его runtime-зависимости будут помещены в `_Build/windows/install`.

### Сборка в Linux

Установите инструментарий и библиотеки, необходимые встроенному SDL3. Без пакетов разработки для audio, Wayland и udev SDL3 тихо настроится без этих бэкендов, и в результате сборка не будет иметь работающего звука и горячего подключения геймпада:

```bash
sudo apt-get install --no-install-recommends \
  clang lld ninja-build cmake git glslang-tools pkg-config \
  libgl1-mesa-dev libx11-dev libxcursor-dev libxext-dev libxfixes-dev \
  libxi-dev libxrandr-dev libxss-dev libxtst-dev libxkbcommon-dev \
  libasound2-dev libpulse-dev libudev-dev libdbus-1-dev libwayland-dev wayland-protocols
```

Для лаунчера требуется Qt 6 (Concurrent, Network, Widgets) — либо пакеты дистрибутива (`qt6-base-dev`), либо официальная установка Qt.

```bash
git submodule update --init --recursive

cmake -S . -B _Build/linux -G Ninja -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ \
  -DCMAKE_PREFIX_PATH="$Qt6_DIR"

cmake --build _Build/linux --target launcher --parallel
cmake --install _Build/linux --prefix _Build/linux/install
```

На этапе установки библиотеки и плагины Qt копируются рядом с бинарными файлами, поэтому `_Build/linux/install` работает без соответствующего системного Qt. FFmpeg линкуется статически из закреплённого релиза [ядра FFmpeg KytyPS5](https://github.com/KytyPS5/ext-ffmpeg-core), включая поддержку VP9 и WebM. Системные пакеты FFmpeg не требуются.

Чтобы собрать `kyty_emulator` и цель `kyty_tests` без Qt, используйте отдельный каталог сборки:

```bash
git submodule update --init --recursive

cmake -S . -B _Build/linux-no-qt -G Ninja -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ \
  -DKYTY_BUILD_LAUNCHER=OFF

cmake --build _Build/linux-no-qt --target kyty_emulator kyty_tests --parallel
```

Как и в Windows, компилятор MSVC не используется; требуется Clang. `cl.exe` отклоняется на этапе настройки.

Корень исходников CMake — это корень репозитория.

### Сборка в NixOS

Оболочка разработки предоставляет Clang, CMake, Ninja, Qt 6, заголовки Vulkan и библиотеки бэкендов SDL3. Войдите в неё и настройте так же, как в других дистрибутивах Linux; оболочка экспортирует `CMAKE_PREFIX_PATH` и `QT_PLUGIN_PATH`, поэтому аргумент `-DCMAKE_PREFIX_PATH="$Qt6_DIR"` не нужен:

```bash
nix-shell # or: nix develop
git submodule update --init --recursive

cmake -S . -B _Build/linux -G Ninja -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++

cmake --build _Build/linux --target launcher --parallel
cmake --install _Build/linux --prefix _Build/linux/install
```

На этапе настройки скачиваются предварительно собранные FFmpeg и исходники `xbyak`, `zydis`, `zstd` и ZArchive, поэтому требуется доступ к сети; для полностью изолированного `nix build` потребовалось бы включить эти входные данные в vendor. Во время выполнения должен быть доступен драйвер Vulkan 1.3 (в NixOS — `hardware.graphics.enable = true`).

### Сборка в macOS

Сборки для macOS ориентированы на x86-64 и работают под Rosetta 2 на Apple Silicon, поэтому x86-64 код игр PS5 выполняется через тот же слой трансляции, что и сам эмулятор. Готовые архивы прикреплены к релизам; шаги ниже предназначены для сборки из исходников.

Требования:

- Mac на Apple Silicon с установленной Rosetta 2 (`softwareupdate --install-rosetta`)
- Xcode (или Command Line Tools)
- Пакеты Homebrew: `brew install cmake ninja glslang`
- Qt 6 (Concurrent, Network, Widgets) с поддержкой x86-64. Официальная установка Qt универсальна и работает; Qt из Homebrew только arm64 и не слинкуется

```bash
git submodule update --init --recursive

cmake -S . -B _Build/macos -G Ninja -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_OSX_ARCHITECTURES=x86_64 \
  -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ \
  -DCMAKE_PREFIX_PATH="$Qt6_DIR"

cmake --build _Build/macos --target launcher --parallel
cmake --install _Build/macos --prefix _Build/macos/install
```

При сборке `kyty_emulator` повторно подписывается с JIT-правами, необходимыми для выполнения транслированного гостевого кода; ручной шаг подписи не требуется. Когда собирается лаунчер, установка также создаёт `_Build/macos/install/KytyPS5.app` — дважды щёлкните, чтобы запустить GUI. Плоский `kyty_emulator` сохраняется для использования из CLI.

Vulkan берётся из MoltenVK. Скачайте `MoltenVK-macos.tar` из [релизов MoltenVK](https://github.com/KhronosGroup/MoltenVK/releases), затем скопируйте `MoltenVK/dynamic/dylib/macOS/libMoltenVK.dylib` рядом с плоским `kyty_emulator` (а для бандла — в `KytyPS5.app/Contents/Frameworks/`) и подпишите ad-hoc:

```bash
codesign --force --sign - _Build/macos/install/libMoltenVK.dylib
# For the bundle (if present):
codesign --force --sign - _Build/macos/install/KytyPS5.app/Contents/Frameworks/libMoltenVK.dylib
codesign --force --sign - _Build/macos/install/KytyPS5.app
```

Релизные архивы уже включают подписанный `libMoltenVK.dylib` (как плоский, так и внутри бандла).

### Регрессионные тесты

Соберите все регрессионные исполняемые файлы и запустите зарегистрированные тесты с помощью:

```powershell
cmake --build _Build/windows --target kyty_tests
ctest --test-dir _Build/windows --output-on-failure
```

Для сборки в Linux используйте `_Build/linux` вместо `_Build/windows`.

### Visual Studio Code

Готовая конфигурация Visual Studio Code включена в [`.vscode`](.vscode). Она настраивает CMake Tools для сборки проекта с Ninja и `clang-cl` и предоставляет профили запуска как для `launcher.exe`, так и для `kyty_emulator.exe`. Она только для Windows: настройки VS Code не могут выбирать компилятор для каждой платформы, поэтому в Linux настраивайте из командной строки, как показано выше.

Перед использованием:

1. Установите расширения **CMake Tools** и **C/C++** в Visual Studio Code.
2. Обновите `CMAKE_PREFIX_PATH` в [`.vscode/settings.json`](.vscode/settings.json), чтобы указать на вашу установку Qt 6 MSVC.
3. Обновите путь `--game` в [`.vscode/launch.json`](.vscode/launch.json) для профиля **Debug kyty_emulator**.
4. Откройте репозиторий в среде разработчика Visual Studio x64, настройте проект CMake и выберите профиль запуска в **Run and Debug**.

## Запуск

Обновите драйвер графики перед сообщением о проблемах с рендерингом.

Чтобы использовать графический лаунчер:

```powershell
.\_Build\windows\install\launcher.exe
```

```bash
./_Build/linux/install/launcher
```

```bash
open _Build/macos/install/KytyPS5.app  # or double-click in Finder
```

При первом запуске добавьте одну или несколько папок с играми в глобальных настройках. Лаунчер рекурсивно ищет в этих папках каталоги игр, содержащие `eboot.bin`, и дампы игр ZArchive (`.zar`), корень архива которых содержит `eboot.bin`. Выберите обнаруженную игру и запустите её из списка игр. Дампы ZArchive монтируются только для чтения и передаются потоково напрямую; их не нужно предварительно извлекать.

Эмулятор также можно запустить напрямую с легально полученным каталогом игры, ELF-файлом или дампом ZArchive:

```powershell
.\_Build\windows\install\kyty_emulator.exe --game "D:\Games\ExampleGame"
.\_Build\windows\install\kyty_emulator.exe --game "D:\Games\ExampleGame.zar"
```

```bash
./_Build/linux/install/kyty_emulator --game "/games/ExampleGame"
./_Build/linux/install/kyty_emulator --game "/games/ExampleGame.zar"
```

В macOS соседний плоский или входящий в приложение `libMoltenVK.dylib` находится автоматически; переменная окружения не требуется:

```bash
./_Build/macos/install/kyty_emulator --game "/games/ExampleGame"
```

Чтобы переопределить загрузчик Vulkan, задайте `SDL_VULKAN_LIBRARY`:

```bash
SDL_VULKAN_LIBRARY=/path/to/libMoltenVK.dylib ./kyty_emulator --game "/games/ExampleGame"
```

Запустите `kyty_emulator --help`, чтобы увидеть доступные параметры графики, логирования, валидации, профилирования и отладки.

### Использование ИИ

Инструменты ИИ могут использоваться для исследований, обратной разработки и помощи в разработке. Участники должны полностью понимать, проверять и тестировать весь код, который они отправляют, и нести ответственность за его корректность. Общение в репозитории, включая описания pull-request, комментарии к коду и комментарии к issue, должно исходить от человека-участника, а не от автономного ИИ-агента.

Pull-request'ы, включающие работу с помощью ИИ или сгенерированную ИИ, должны раскрывать объём участия ИИ и описывать человеческую проверку и тестирование, выполненные перед отправкой. Непроверенные или непротестированные сгенерированные изменения могут быть закрыты без рассмотрения.

## Лицензия

KytyPS5 лицензирован под [GNU General Public License version 2](LICENSE) (`GPL-2.0-only`).

Этот проект основан на оригинальном [Kyty](https://github.com/InoriRus/Kyty), который был выпущен под лицензией MIT. Оригинальное уведомление об авторских правах и лицензии Kyty сохранено в [`LICENSES/Kyty-MIT.txt`](LICENSES/Kyty-MIT.txt). Сторонние компоненты остаются подчинёнными лицензиям, включённым в эти компоненты.

## Особая благодарность

- [InoriRus/Kyty](https://github.com/InoriRus/Kyty) — KytyPS5 основан на сильно изменённой версии оригинального проекта Kyty.
- [shadps4-emu/shadPS4](https://github.com/shadps4-emu/shadPS4) — справочный материал для понимания поведения памяти PS4, алиасинга ресурсов GPU и когерентности кэша, а также реализации AVPlayer.
