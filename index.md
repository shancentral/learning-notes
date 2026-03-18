- [Agile](https://shancentral.github.io/learning-notes/agile)
- [JS Intricates](https://shancentral.github.io/learning-notes/js-intricates)
- [Interview Refresher](https://shancentral.github.io/learning-notes/interview-refresher)
- [Node Interview](https://shancentral.github.io/learning-notes/node-interview)
- [Flight Booking - Project](https://shancentral.github.io/learning-notes/flight-booking-project)

```js
async function encryptData(plainText, password) {
  const encoder = new TextEncoder();
  const salt = crypto.getRandomValues(new Uint8Array(16));
  const iv = crypto.getRandomValues(new Uint8Array(12)); // Initialization Vector

  // 1. Create a key from the password
  const passwordKey = await crypto.subtle.importKey(
    "raw", encoder.encode(password), "PBKDF2", false, ["deriveKey"]
  );

  // 2. Derive the actual AES key
  const aesKey = await crypto.subtle.deriveKey(
    { name: "PBKDF2", salt, iterations: 100000, hash: "SHA-256" },
    passwordKey,
    { name: "AES-GCM", length: 256 },
    false, ["encrypt"]
  );

  // 3. Encrypt
  const encrypted = await crypto.subtle.encrypt(
    { name: "AES-GCM", iv },
    aesKey,
    encoder.encode(plainText)
  );

  // Return salt + iv + ciphertext as a single Base64 string
  const combined = new Uint8Array(salt.length + iv.length + encrypted.byteLength);
  combined.set(salt, 0);
  combined.set(iv, salt.length);
  combined.set(new Uint8Array(encrypted), salt.length + iv.length);
  
  return btoa(String.fromCharCode(...combined));
}

async function decryptData(cipherText, password) {
  const encoder = new TextEncoder();
  const combined = new Uint8Array(atob(cipherText).split("").map(c => c.charCodeAt(0)));
  
  const salt = combined.slice(0, 16);
  const iv = combined.slice(16, 28);
  const data = combined.slice(28);

  const passwordKey = await crypto.subtle.importKey(
    "raw", encoder.encode(password), "PBKDF2", false, ["deriveKey"]
  );

  const aesKey = await crypto.subtle.deriveKey(
    { name: "PBKDF2", salt, iterations: 100000, hash: "SHA-256" },
    passwordKey,
    { name: "AES-GCM", length: 256 },
    false, ["decrypt"]
  );

  try {
    const decrypted = await crypto.subtle.decrypt({ name: "AES-GCM", iv }, aesKey, data);
    return new TextDecoder().decode(decrypted);
  } catch (e) {
    throw new Error("Decryption failed: Wrong password or corrupted data.");
  }
}
```
