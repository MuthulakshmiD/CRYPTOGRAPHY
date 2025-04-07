# CRYPTOGRAPHY
HILL CIPHER
EX. NO: 1(C) AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.

STEP-2: Multiply the two matrices to obtain the cipher text of length three.

STEP-3: Combine all these groups to get the complete cipher text.

## PROGRAM 

Name : Muthulakshmi D
Reg : 212223040122
```
import numpy as np

def mod_inverse(a, m):
    for i in range(1, m):
        if (a * i) % m == 1:
            return i
    return None

def matrix_mod_inv(matrix, mod):
    det = int(np.round(np.linalg.det(matrix)))
    det_inv = mod_inverse(det % mod, mod)
    if det_inv is None:
        raise ValueError("Matrix is not invertible")
    adjugate = np.round(det * np.linalg.inv(matrix)).astype(int) % mod
    return (det_inv * adjugate) % mod

def text_to_numbers(text):
    return [ord(char) - 65 for char in text]

def numbers_to_text(numbers):
    return ''.join(chr((num % 26) + 65) for num in numbers)

def hill_cipher_encrypt(plaintext, key_matrix):
    plaintext = plaintext.upper().replace(" ", "")
    while len(plaintext) % 3 != 0:
        plaintext += 'X'
    plaintext_numbers = text_to_numbers(plaintext)
    plaintext_matrix = np.array(plaintext_numbers).reshape(-1, 3).T
    encrypted_matrix = (np.dot(key_matrix, plaintext_matrix) % 26).T
    return numbers_to_text(encrypted_matrix.flatten())

def hill_cipher_decrypt(ciphertext, key_matrix):
    key_matrix_inv = matrix_mod_inv(key_matrix, 26)
    ciphertext_numbers = text_to_numbers(ciphertext)
    ciphertext_matrix = np.array(ciphertext_numbers).reshape(-1, 3).T
    decrypted_matrix = (np.dot(key_matrix_inv, ciphertext_matrix) % 26).T
    return numbers_to_text(decrypted_matrix.flatten())

key_matrix = np.array([[1, 2, 1], [2, 3, 2], [2, 2, 1]])
plaintext = input("Enter plaintext: ")
ciphertext = hill_cipher_encrypt(plaintext, key_matrix)
print("Encrypted text:", ciphertext)
decrypted_text = hill_cipher_decrypt(ciphertext, key_matrix)
print("Decrypted text:", decrypted_text)
```
## OUTPUT
![424296684-800e3725-584f-4a72-98ab-45d50ad2f281](https://github.com/user-attachments/assets/d07cefa3-0556-4002-8b78-26499f6dc95d)

## RESULT
   The program is executed successfully
