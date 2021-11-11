Ответы на вопросы:  
1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.  
Команда:  
```
git show aefea
``` 
   **aefead2207ef7e2aa5dc81a34aedf0cad4c32545** (полный хэш коммита)  
   **Update CHANGELOG.md** (комментарий к коммиту)


2. Какому тегу соответствует коммит 85024d3?  
Команда: 
```
git show 85024d3
```
коммит соответствует тегу **v0.12.23**


3. Сколько родителей у коммита b8d720? Напишите их хеши.  
Команда: 
```
git cat-file -p b8d720
```
   У коммита **b8d720** 2 родителя с хэшами:  
      **56cd7859e05c36c06b56d013b55a252d0bb7e158**  
      **9ea88f22fc6269854151c571162c5bcf958bee2b**
   
А также можно выполнить команду
```
git log --pretty=%P -n 1 b8d720
```
которая также покажет 2 родителя  


4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.  
Команда:  
   ```
   git log --oneline --graph v0.12.23..v0.12.24
   ```
   Результат выполнения:  
   ```
   33ff1c03b (tag: v0.12.24) v0.12.24
   b14b74c49 [Website] vmc provider links
   3f235065b Update CHANGELOG.md
   6ae64e247 registry: Fix panic when server is unreachable
   5c619ca1b website: Remove links to the getting started guide's old location
   06275647e Update CHANGELOG.md
   d5f9411f5 command: Fix bug when using terraform login on Windows
   4b6d06cc5 Update CHANGELOG.md
   dd01a3507 Update CHANGELOG.md
   225466bc3 Cleanup after v0.12.23 release
   ```  
5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).  
Команда:
```
git log -S"func providerSource("
```
Результат:
```
commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700
```

ИЛИ  
Команда:
```
git grep "func providerSource"
```
Вывод:
```
provider_source.go:func providerSource(configs []*cliconfig.ProviderInstallation, services *disco.Disco) (getproviders.Source, tfdiags.Diagnostics) {
```
Затем
```
git log --reverse provider_source.go
```
Результат:
```
commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700
```


6. Найдите все коммиты в которых была изменена функция globalPluginDirs.  
Команда:
```
git grep "func globalPluginDirs"
```
Результат:
```
commands.go:            GlobalPluginDirs: globalPluginDirs(),
commands.go:    helperPlugins := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())
internal/command/cliconfig/config_unix.go:              // FIXME: homeDir gets called from globalPluginDirs during init, before
plugins.go:// globalPluginDirs returns directories that should be searched for
plugins.go:func globalPluginDirs() []string {
```
Функция определяется только в файле plugins.go.
Затем:
```
git log -L :globalPluginDirs:plugins.go --oneline
```
Результат:
```
78b122055 Remove config.go and update things using its aliases
52dbf9483 keep .terraform.d/plugins for discovery
41ab0aef7 Add missing OS_ARCH dir to global plugin paths
66ebff90c move some more plugin search path logic to command
8364383c3 Push plugin discovery down into command package
```

7. Кто автор функции synchronizedWriters?  
**Martin Atkins**  
Команда:
```
git log -SsynchronizedWriters --reverse
```
Результат:
```
commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Wed May 3 16:25:41 2017 -0700
```