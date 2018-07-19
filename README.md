# iOSProjectSetup
Создание и настройка нового проекта.

### 0. ВНИМАНИЕ! Данный пункт необходимо выполнять только в том случае, если на вашем Mac не установлены данные утилиты

Установите HomeBrew с помощью команды:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)» 
```

Установите swiftlint с помощью команды: 
```
brew install swiftlint
```

Установите cocoapods с помощью команды: 
```
sudo gem install cocoapods 
```

### 1. Добавьте в корневой каталог проекта файлы .swiftlint.yml и .gitignore. 

### 2. Во вкладке Build Phases добавьте новый скрипт Highlight со следующим содержанием:
```
TAGS="TODO:|FIXME:"
SKIPDIRS="/Pods"
find "${SRCROOT}/" -type f \( -name "*.h" -or -name "*.m" -or -name "*.swift" \) -print0 \
| xargs -0 egrep --with-filename --line-number --only-matching "($TAGS).*\$" \
| grep -v "$SKIPDIRS" \
| perl -p -e "s/($TAGS)/ warning: \$1/"
```

### 3. Добавьте еще один скрипт Swiftlint со следующим содержанием:
```
if which swiftlint >/dev/null; then
swiftlint
else
echo "error: SwiftLint does not exist, download it from https://github.com/realm/SwiftLint"
exit 1
fi
```
данный скрипт обеспечивает работу статического анализатора кода swiftlint.

### 4. В терминале перейдите в корневую папку проекта и выполните команды `pod init` и `pod install`, после инициализации Podfile откройте workspace файл и примените рекомендуемые Xcode изменения.
