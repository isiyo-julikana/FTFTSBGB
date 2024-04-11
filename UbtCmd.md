# 1. Использование команды cat в Linux
   - Создать два текстовых файла: "Pets"(Домашние животные) и "Pack animals"(вьючные животные), используя команду `cat` в терминале Linux. В первом файле перечислить собак, кошек и хомяков. Во втором — лошадей, верблюдов и ослов.
   - Объединить содержимое этих двух файлов в один и просмотреть его содержимое.
   - Переименовать получившийся файл в "Human Friends".

```
isiyojulicana@uij:~$ mkdir FT
isiyojulicana@uij:~$ cd FT
isiyojulicana@uij:~/FT$ cat > Pets
Dog
Cat  
Hamsters
isiyojulicana@uij:~/FT$ cat > PackAnimals
Horse
Camel
Donkey
isiyojulicana@uij:~/FT$ cat Pets PackAnimals > Menagerie
isiyojulicana@uij:~/FT$ cat Menagerie
Dog
Cat
Hamsters
Horse
Camel
Donkey
isiyojulicana@uij:~/FT$ mv Menagerie HumanFriends
isiyojulicana@uij:~/FT$ ls
HumanFriends  PackAnimals  Pets
isiyojulicana@uij:~/FT$  
```

---
# 2. Работа с директориями в Linux
   - Создать новую директорию и переместить туда файл "Human Friends".

```
isiyojulicana@uij:~/FT$ mkdir NewDir
isiyojulicana@uij:~/FT$ mv HumanFriends NewDir
isiyojulicana@uij:~/FT$ ls
NewDir  PackAnimals  Pets
isiyojulicana@uij:~/FT$ cd NewDir
isiyojulicana@uij:~/FT/NewDir$ ls
HumanFriends
isiyojulicana@uij:~/FT/NewDir$ cat HumanFriends
Dog
Cat
Hamsters
Horse
Camel
Donkey
isiyojulicana@uij:~/FT/NewDir$ cd .. 
isiyojulicana@uij:~/FT$ 
```

---
# 3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину ”
   - Подключить дополнительный репозиторий MySQL и установить один из пакетов из этого репозитория.

```
isiyojulicana@uij:~/FT$ wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb
isiyojulicana@uij:~/FT$ sudo apt install ./mysql-apt-config_0.8.12-1_all.deb -y
isiyojulicana@uij:~/FT$ sudo apt install mysql-client -y
```

---
# 4. Управление deb-пакетами
   - Установить и затем удалить deb-пакет, используя команду `dpkg`.

  ```
isiyojulicana@uij:~/FT$ wget https://download3.operacdn.com/pub/opera/desktop/109.0.5097.45/linux/opera-stable_109.0.5097.45_amd64.deb
isiyojulicana@uij:~/FT$ sudo dpkg -i opera-stable_109.0.5097.45_amd64.deb
isiyojulicana@uij:~/FT$ sudo dpkg -S /usr/bin/opera
opera-stable: /usr/bin/opera
isiyojulicana@uij:~/FT$ sudo dpkg --purge opera-stableё
  ```

   ---
