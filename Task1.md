import hashlib
import os

# Function to calculate the SHA-256 hash of a file
def calculate_hash(file_path):
    sha256_hash = hashlib.sha256()
    try:
        with open(file_path, "rb") as f:
            # Read and update hash in chunks
            for byte_block in iter(lambda: f.read(4096), b""):
                sha256_hash.update(byte_block)
        return sha256_hash.hexdigest()
    except FileNotFoundError:
        print("File not found!")
        return None

# Save the hash to a file for future comparison
def save_hash(file_path, hash_value):
    with open(file_path + ".hash", "w") as f:
        f.write(hash_value)

# Read the stored hash value
def read_saved_hash(file_path):
    try:
        with open(file_path + ".hash", "r") as f:
            return f.read()
    except FileNotFoundError:
        return None

# Main function to check integrity
def check_integrity(file_path):
    current_hash = calculate_hash(file_path)
    if current_hash is None:
        return

    saved_hash = read_saved_hash(file_path)

    if saved_hash is None:
        print("No saved hash found. Saving current hash...")
        save_hash(file_path, current_hash)
        print("Hash saved successfully.")
    else:
        if current_hash == saved_hash:
            print("File integrity verified. No changes detected.")
        else:
            print("WARNING: File has been modified!")

# === Run This ===
file_path = input("Enter the path to the file you want to check: ")
check_integrity(file_path)
