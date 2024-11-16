# Less Secure Client-Side Login

# 1.Login Page:
-userHash is generated as a SHA-256 hash of the username and password.
-userHash is used to derive an AES key.
-A session token ("adminToken") is encrypted with the derived AES key and stored in sessionStorage.
-userHash is added to the URL and stored in sessionStorage as a backup.

# 2.Admin Page:
-userHash is retrieved from the URL and matched with sessionStorage.
-The AES key is re-derived from userHash, and the session token is decrypted.
-Access is granted only if the decrypted token matches the expected token.

# 3.Benefits of This Setup:
--Secure URL Identification: userHash in the URL identifies the session without exposing the actual session token.
--Encrypted Validation: Encrypting the session token prevents unauthorized users from simply copying the token to gain access.
--Deterministic Key Derivation: Re-deriving the AES key from userHash ensures that the same encryption key is used consistently without storing it directly.

# 4.Limitations:
This setup strengthens the client-side security by combining deterministic hashing with AES encryption. However, for production, server-side validation would still be necessary for complete security. This is suitable for demo only or for a simple login page that doesn't require high-security measures.