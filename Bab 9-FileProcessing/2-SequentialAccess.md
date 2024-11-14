[<< Pengantar File Processing](1-Pengantar.md)

# 9.2 - Sequential Access

**Sequential access** menyimpulkan bahwa file dapat direpresentasikan sebagai kumpulan karakter atau bytes yang panjangnya tidak diketahui. File berjenis **plaintext** umumnya dioperasikan secara sequential access. Dengan demikian, pembahasan seputar topik ini hanya seputar file berjenis plaintext saja.

## Operasi Pembacaan (Read)

Dalam membaca file berjenis plaintext, dapat menggunakan beberapa fungsi pada header **stdio.h** seperti: `fscanf`, `fgetc`, dan `fgets`. Cara penggunaan tiap-tiap fungsi tersebut dapat dilihat [di sini](https://cplusplus.com/reference/cstdio/).

Namun dalam kali ini kita akan membahas yang `fscanf` saja. Pada dasarnya, `fscanf` memiliki kinerja yang hampir mirip dengan fungsi `scanf`. Perhatikan contoh berikut:

Isi file **biodata.txt** sebelumnya:
```
Farhan_Wegig_ALIAS_TIOBIGBOAY
Sains_Data
2023
```

```c
#include <stdio.h>

int main() {
    FILE *f;

    printf("Memuat dari apalah.txt ...");
    f = fopen("apalah.txt", "r");
    if (f != NULL) {
        char nama[100];
        char prodi[50];
        int angkatan;

        // Membaca data dari file
        fscanf(f, "%s", nama);       // Membaca nama
        fscanf(f, "%s", prodi);      // Membaca program studi
        fscanf(f, "%d", &angkatan);  // Membaca angkatan

        // Menampilkan data yang dibaca
        printf("\nNama : %s\n", nama);
        printf("Prodi : %s\n", prodi);
        printf("Angkatan : %d\n", angkatan);

        fclose(f);  // Menutup file setelah selesai
    } else {
        // Menampilkan pesan jika file tidak dapat dibuka
        printf("\nTidak dapat membaca file biodata.txt\n");
    }

    return 0;
}
```

## Operasi Penulisan (Write)

Dalam menulis file berjenis plaintext, dapat menggunakan beberapa fungsi pada header **stdio.h** seperti: `fprintf`, `fputc`, dan `fputs`. Cara penggunaan tiap-tiap fungsi tersebut dapat diliht [di sini](https://cplusplus.com/reference/cstdio/)

```c
#include <stdio.h>

int main() {
FILE *f;
char nama[100];
char prodi[50];
int angkatan;

printf("Masukkan nama : ");
scanf("%s", nama);

printf("Masukkan prodi : ");
scanf("%s", prodi);

printf("Masukkan angkatan : ");
scanf("%d", &angkatan);

printf("Menyimpan ke biodata.txt ...\n");
f = fopen("biodata.txt", "w");
if (f != NULL) {
    fprintf(f, "%s\n", nama);
    fprintf(f, "%s\n", prodi);
    fprintf(f, "%d\n", angkatan);
    fclose(f);
    printf("Sukses!\n");
} else {
    printf("Tidak dapat menulis ke file biodata.txt");
}
}
/*
Output:

Masukkan nama : Windah
Masukkan prodi : Sadat
Masukkan angkatan : 2023
Menyimpan ke biodata.txt ...
Sukses!
*/
```

Isi file **biodata.txt** setelahnya:
```
Windah
Sadat
2023
```

## Rewind

Kursor yang merujuk ke lokasi target operasi pembacaan/penulisan berikutnya dalam file sequential-access (plaintext) dapat direset menggunakan fungsi **rewind()** pada **stdio.h** dengan deklarasi sebagai berikut:
```c
void rewind(FILE *f);
```
Fungsi tersebut mengatur kursor pada file `f` supaya dikembalikan ke lokasi kursor pada awal file.

Namun patut diperhatikan bahwa operasi penulisan setelah dilakukan rewind dapat merusak representasi data yang ada di dalam file. Oleh karena itu, gunakanlah saja dengan berhati-hati apabila akan melibatkan penulisan ke dalam file lagi.

Sebagai contoh:
```c
FILE *f;

/* ... */

fprintf(f, "Lorem ipsum dolor\n");
rewind(f);
fprintf(f, "sit amet\n");
```

[Random Access >>](3-RandomAccess.md)
