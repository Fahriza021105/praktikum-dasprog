# praktikum-dasprog
# Program Kasir Sederhana dalam C

Program ini adalah sistem kasir sederhana yang ditulis dalam bahasa C. Program menerima input berupa nama barang, harga, dan jumlah barang, kemudian menghasilkan struk belanja yang mencakup total harga, diskon (jika ada), dan total akhir setelah diskon.

## Fitur
- **Input Barang**: Pengguna dapat memasukkan hingga maksimal 20 item. Setiap item terdiri dari nama, harga, dan jumlah.
- **Dukungan Diskon**: Program ini mendukung penerapan diskon dalam bentuk persentase pada total belanja. Jika tidak ada diskon, program akan mencetak total penuh tanpa potongan.
- **Tampilan Struk**: Program menampilkan struk yang detail, termasuk:
  - Nama barang, jumlah, dan subtotal untuk setiap barang.
  - Total sebelum diskon.
  - Diskon yang diterapkan (jika ada).
  - Total akhir setelah diskon.

## Cara Menggunakan
1. Kompilasi program menggunakan kompiler C
2. Jalankan program yang sudah dikompilasi
3. Masukkan jumlah item yang ingin dibeli (maksimal 10).
4. Untuk setiap item, masukkan nama barang, harga, dan jumlah.
5. Setelah memasukkan semua item, tentukan diskon dalam bentuk persentase (masukkan 0 jika tidak ada diskon).
6. Struk belanja akan ditampilkan dengan semua rincian, termasuk total sebelum dan setelah diskon.


berikut kode nya


        #include <stdio.h>
      #include <string.h> // Untuk menggunakan fungsi strlen
      
      #define MAX_ITEMS 10 // Mendefinisikan konstanta yang berupa item maksimal yang bisa ditampilkan
      
      typedef struct { // Mendefinisikan struktur baru yaitu (Item) yang memiliki tiga atribut yaitu nama, harga, dan jumlah
          char nama[30];
          float harga;
          int jumlah;
      } Item; // Nama dari struktur baru yaitu Item
      
      void tampilkanStruk(Item items[], int count, float diskon) { 
          float total = 0.0; // Variabel total untuk menyimpan total harga sebelum terkena diskon
          printf("============= Struk Belanja =========== \n");
          printf("============= Toko Fahriza  ===========\n");
    
    for (int i = 0; i < count; i++) { // Loop untuk setiap item
        float subtotal = items[i].harga * items[i].jumlah; // Hitung subtotal
        printf("%s (x%d): %.2f\n", items[i].nama, items[i].jumlah, subtotal); // Tampilkan nama item, jumlah, dan subtotal
        total += subtotal; // Tambahkan subtotal ke total keseluruhan
    }
    
    printf("=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-= \n");
    printf("Total Sebelum Diskon: %.2f \n", total);
    
    if (diskon > 0) { // Jika ada diskon
        float totalDiskon = total * (diskon / 100); // Hitung total diskon
        total -= totalDiskon; // Kurangi total dengan total diskon
        printf("Total Diskon\t: %.2f%%\n", diskon);
        printf("Total Setelah Diskon: %.2f \n", total);
    } else { // Jika tidak ada diskon
        printf("Tidak ada diskon.\n");
        printf("Total Setelah Diskon: %.2f\n", total);
    }
      }
      
      // Fungsi utama program
      int main() {
          Item items[MAX_ITEMS]; 
          int count = 0;
          float diskon;

    printf("Masukkan jumlah item (maksimal %d): ", MAX_ITEMS);
    scanf("%d", &count);

    // Validasi jumlah item agar tidak melebihi batas
    if (count > MAX_ITEMS) {
        printf("Jumlah item melebihi batas maksimal (%d).\n", MAX_ITEMS);
        return 1; // Keluar dari program jika melebihi batas
    }

    getchar(); // Membersihkan newline dari buffer

    for (int i = 0; i < count; i++) {
        printf("Masukkan nama item %d: ", i + 1);
        fgets(items[i].nama, sizeof(items[i].nama), stdin);
        items[i].nama[strcspn(items[i].nama, "\n")] = '\0'; // Menghilangkan newline di akhir input
        
        printf("Masukkan harga item %d: ", i + 1);
        scanf("%f", &items[i].harga);
        
        printf("Masukkan jumlah item %d: ", i + 1);
        scanf("%d", &items[i].jumlah);

        getchar(); // Membersihkan newline setelah setiap scanf
    }

    printf("Masukkan diskon (dalam persen, 0 jika tidak ada): ");
    scanf("%f", &diskon);

    tampilkanStruk(items, count, diskon); // Memanggil fungsi tampilkanStruk untuk mengoutput struk belanja

    return 0;
    }
