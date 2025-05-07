#Advance Encryption Tool( AES-256)
from cryptography.fernet import Fernet

# Generate key (save it securely!)
def generate_key():
    key = Fernet.generate_key()
    with open("key.key", "wb") as key_file:
        key_file.write(key)

def load_key():
    return open("key.key", "rb").read()

def encrypt_file(filename, key):
    fernet = Fernet(key)
    with open(filename, "rb") as file:
        original = file.read()

    encrypted = fernet.encrypt(original)
    with open(filename + ".enc", "wb") as file:
        file.write(encrypted)

def decrypt_file(filename, key):
    fernet = Fernet(key)
    with open(filename, "rb") as file:
        encrypted = file.read()

    decrypted = fernet.decrypt(encrypted)
    with open("decrypted_" + filename.replace(".enc", ""), "wb") as file:
        file.write(decrypted)

# Usage
generate_key()  # Run once
key = load_key()
encrypt_file("test.txt", key)
decrypt_file("test.txt.enc", key)
