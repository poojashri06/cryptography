def frequency_attack(ciphertext, top_n=10):
    alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    letter_freq = {letter: 0 for letter in alphabet}
    for letter in ciphertext:
        if letter.isalpha():
            letter_freq[letter.upper()] += 1
    sorted_freq = sorted(letter_freq.items(), key=lambda x: x[1], reverse=True)
    most_freq_letter = sorted_freq[0][0]
    shift = (ord(most_freq_letter) - ord('E')) % 26
    def decrypt(ciphertext, shift):
        decrypted_text = ""
        for letter in ciphertext:
            if letter.isalpha():
                base = ord('A') if letter.isupper() else ord('a')
                decrypted_text += chr((ord(letter) - base - shift) % 26 + base)
            else:
                decrypted_text += letter
        return decrypted_text
    possible_plaintexts = [decrypt(ciphertext, shift)]
    for i in range(1, top_n):
        possible_plaintexts.append(decrypt(ciphertext, (shift + i) % 26))
    return possible_plaintexts
ciphertext = "Lzw esp pwtwz hzv hszg ptwspz aljrljbz!"
top_n = 10
possible_plaintexts = frequency_attack(ciphertext, top_n)
for i, plaintext in enumerate(possible_plaintexts, 1):
    print(f"Plaintext {i}: {plaintext}")
