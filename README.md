# Potrzebne narzędzia

### Biblioteki:
```c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <semaphore.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <stdint.h>
#include <unistd.h>
#include <string.h>
```

### CMakeLists:
```
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package( Threads REQUIRED )
target_link_libraries(<catalogue_name> PRIVATE Threads::Threads librt.so)
```

### Komenda do manualnej kompilacji:
```
gcc -pthread -lrt <source_file> -o <output_file>
```


# Postawienie pamięci współdzielonej

Do postawienia pamięci korzystamy z 3 funkcji (najlepiej w tej kolejności):

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

---
# Bardziej szczegółówe opisy funkcji
## `shm_open`
### Flags
- `O_RDONLY` - obiekt można tylko czytać
- `O_RDWR` - obiekt można czytać i modyfikować
- `O_CREAT` - tworzy obiekt jeśli nie istnieje, lub go otwiera
- `O_CREAT | O_EXCL` - tworzy nowy obiekt lub zwraca błąd jeśli taki istnieje
- `O_CREAT | O_RDWR` - tworzymy obiekt który możemy edytować
### Modes
- `0666` - każdy ma dostęp
- `0600` - tylko właściciel
### Return value
- `>= 0` - jeśli sukces
- `-1` - jeśli błąd
