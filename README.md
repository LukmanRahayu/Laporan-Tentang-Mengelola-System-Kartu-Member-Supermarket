# Laporan-Tentang-Mengelola-System-Kartu-Member-Supermarket
import getpass

# Database sementara dalam bentuk dictionary
users = {}

def register():
    print("\n=== Registrasi ===")
    nama = input("Masukkan Nama Lengkap: ")
    password = getpass.getpass("Buat Kata Sandi: ")

    if nama in users:
        print("Nama sudah terdaftar!")
    else:
        users[nama] = {"password": password, "poin": 0}
        print("Registrasi berhasil! Silakan login.")

def login():
    print("\n=== Login ===")
    nama = input("Masukkan Nama: ")
    password = getpass.getpass("Masukkan Kata Sandi: ")

    if nama in users and users[nama]["password"] == password:
        print(f"Login berhasil! Selamat datang, {nama}")
        return nama
    else:
        print("Login gagal!")
        return None

def tambah_transaksi(nama):
    jumlah = float(input("Masukkan jumlah transaksi: "))
    users[nama]["poin"] += int(jumlah // 10000 * 10)
    print(f"Transaksi berhasil! Poin saat ini: {users[nama]['poin']}")

def tukar_poin(nama):
    print("\n1. Diskon Rp5.000 (50 poin)")
    print("2. Diskon Rp10.000 (100 poin)")
    pilihan = input("Pilih hadiah: ")

    if pilihan == "1" and users[nama]["poin"] >= 50:
        users[nama]["poin"] -= 50
        print("Diskon Rp5.000 berhasil digunakan!")
    elif pilihan == "2" and users[nama]["poin"] >= 100:
        users[nama]["poin"] -= 100
        print("Diskon Rp10.000 berhasil digunakan!")
    else:
        print("Poin tidak cukup!")

def lihat_profil(nama):
    print(f"\n=== Profil {nama} ===")
    print(f"Poin: {users[nama]['poin']}")

def main():
    while True:
        print("\n1. Login\n2. Registrasi\n3. Keluar")
        pilihan = input("Pilih menu: ")

        if pilihan == "1":
            nama = login()
            if nama:
                while True:
                    print("\n1. Tambah Transaksi\n2. Tukar Poin\n3. Lihat Profil\n4. Logout")
                    sub_pilihan = input("Pilih menu: ")

                    if sub_pilihan == "1":
                        tambah_transaksi(nama)
                    elif sub_pilihan == "2":
                        tukar_poin(nama)
                    elif sub_pilihan == "3":
                        lihat_profil(nama)
                    elif sub_pilihan == "4":
                        break
        elif pilihan == "2":
            register()
        elif pilihan == "3":
            print("Terima kasih!")
            break

if __name__ == "__main__":
    main()
