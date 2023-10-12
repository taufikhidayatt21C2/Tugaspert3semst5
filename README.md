# Tugaspert3semst5
Taufik Hidayat,312110066,T21.C2 Pert3.
def vigenere_cipher(text, key, mode):
    result = ""
    key_length = len(key)
    for i in range(len(text)):
        char = text[i]
        if char.isalpha():
            key_char = key[i % key_length]
            if char.isupper():
                shift = ord('A')
            else:
                shift = ord('a')
            if mode == 'encrypt':
                result += chr((ord(char) - shift + ord(key_char) - shift) % 26 + shift)
            elif mode == 'decrypt':
                result += chr((ord(char) - shift - (ord(key_char) - shift)) % 26 + shift)
        else:
            result += char
    return result

def create_account(username, password, key):
    # Enkripsi password dengan Vigenere Cipher
    encrypted_password = vigenere_cipher(password, key, 'encrypt')

    # Simpan username dan password terenkripsi ke database atau file
    user_data = f"{username}:{encrypted_password}\n"
    with open("user_database.txt", "a") as file:
        file.write(user_data)

def login(username, password, key):
    # Baca data dari database atau file
    with open("user_database.txt", "r") as file:
        for line in file:
            stored_username, stored_password = line.strip().split(':')
            if username == stored_username:
                # Dekripsi password terenkripsi dari database
                decrypted_password = vigenere_cipher(stored_password, key, 'decrypt')
                if password == decrypted_password:
                    return True
    return False

# Penggunaan:
key = "kunci_vigenere"
username = "taufik"
password = "12345"

# Registrasi akun
create_account(username, password, key)

# Verifikasi Login
login_username = input("Masukkan username: ")
login_password = input("Masukkan password: ")

if login(login_username, login_password, key):
    print("Login berhasil.")
else:
    print("Login gagal.")
![image](https://github.com/taufikhidayatt21C2/Tugaspert3semst5/assets/116345854/d3303a7d-6b9c-4b62-84f2-7e28a133098a)

