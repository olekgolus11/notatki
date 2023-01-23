# Postawienie pamięci współdzielonej

Do postawienia pamięci korzystamy z 3 funkcji:

Funkcja tworząca pamięć współdzieloną:
```c
int file_descriptor = shm_open(<file_name>, <flags>, <mode>);
```

Funkcja tworząca miejsce na tę pamięć:
```c
ftruncate(<file_descriptor>, <size of structure>);
```

Funkcja mapująca nasz obiekt na tę pamięć:
```c
struct My_structure* my_structure = mmap(<address>, <size of structure>, <protection flags>, <file_descriptor>, <offset>);
```

# Usunięcie pamięci współdzielonej:

Funkcja odmapowująca nasz obiekt z pamięci:
```c
munmap(<pointer to structure>, <size of structure>);
```

Funkcja usuwająca pamięć współdzieloną:
```c
shm_unlink(<file_name>);
```
