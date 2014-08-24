soda
====

...	...	@@ -1,4 +1,23 @@
1		-iPhone-Baseband-Memory-Decryptor
1	+iPhone Baseband Decryptor
2	2	 ================================
3	3	 
4		-When testing a network code key, the baseband firmware reads the encryptedSignature, calculates the deviceKey and the nckKey from the entered NCK, decrypts the encryptedSignature with the nckKey using TEA, decrypts it once more with the public RSA key and verifies the signature with the SHA1 hashes of the chipID / norID.
5	4	\ No newline at end of file
5	+When testing a network code key, the baseband firmware reads the encryptedSignature, calculates the deviceKey and the nckKey from the entered NCK, decrypts the encryptedSignature with the nckKey using TEA, decrypts it once more with the public RSA key and verifies the signature with the SHA1 hashes of the chipID / norID.
6	+
7	+Two identification numbers unique to each device are generated from the NOR flash and baseband CPU serials: the norID and the chipID, 8 respectively 12 bytes in size.
8	+The device-specific deviceKey is generated from truncating a SHA1 hash of the concatenated and padded norID and chipID.
9	+A supposedly random NCK (�network control key�) is SHA1-hashed. With the hashed NCK and the norID and chipID, the second key nckKey is generated. The hashing algorithm uses Tiny Encryption Algorithm (TEA). The nckKey is also device-specific since both the norID and chipIDare used.
10	+A device-specific RSA signature is generated: two SHA1 hashes are generated from the norID and chipID. The status that the lock has after the correct NCK has been entered is also embedded into this message. The PCKS 1.5 format is used to pad the hashes and the status from (2*160+32) bit to 2048 bit (256 byte).
11	+The asymmetric RSA algorithm is used for the encryption of the unlock signature. Keep in mind that the algorithm uses two different keys: a private key for encryption and a public key for decryption. With the private RSA key, the signature is encrypted and stored in protected memory.
12	+This signature is encrypted with TEA once again using the device-specific deviceKey in CBC mode.
13	+
14	+This script will extract all tokens, required to have memory dumped into binary file.
15	+================================
16	+Here is Dev-team NOR Dumper implementation/
17	+http://www.letsunlockiphone.com/dump-iphone-baseband-nor-memory-nordumper/
18	+
19	+Sample of using this script:
20	+================================
21	+http://www.letsunlockiphone.com/dump-iphone-baseband-nor-memory-nordumper/
22	+
23	+Big thanks to @Dogbert for awesome script.
24	+http://dogber1.blogspot.com
6	25	\ No newline at end of file
