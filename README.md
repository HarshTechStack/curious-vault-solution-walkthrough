

````markdown
# 🔐 Curious Vault Challenge — Solution Walkthrough (90% Completed)

> ⚡ **Challenge yourself first!** Before reading further, try visiting the [Curious Vault](https://workwithus.webminix.com) yourself and explore `/begin`. See how far you can go before comparing your path with mine. This puzzle is a real test of your problem-solving and web exploration skills.

This repository documents my personal exploration of the Curious Vault Challenge by Webminix. It was an immersive technical puzzle that involved DNS records, HTTP headers, encoding, and cryptic clues — an ideal challenge for problem-solvers.

> ❗ **Disclaimer**: This is *not* a spoiler repository. The walkthrough explains my thought process and commands without revealing the final working solution. This effort demonstrates my technical reasoning and debugging approach.

---

## 🎯 Objective

Unlock the `/open` endpoint by discovering and using a hidden passphrase found via API calls and DNS.

---

## 🛠 Tools Used

* `curl` for making API requests
* `dig` for DNS record lookups
* Shell scripting for automation
* Base64 and SHA256 utilities
* Logical deduction, API header manipulation

---

## 🚶 Step-by-Step Breakdown

### 🔹 Step 1: Initiate the Puzzle

```bash
curl -X GET "https://workwithus.webminix.com/begin"
```

**Response:** A base64-encoded riddle hinting to use a specific `User-Agent`: `Curious_Explorer`.

---

### 🔹 Step 2: Obtain the Key

```bash
curl -X POST "https://workwithus.webminix.com/find-key" \
  -H "User-Agent: Curious_Explorer" \
  -H "X-Forwarded-Host: webminix.com" \
  -H "X-Requested-With: XMLHttpRequest"
```

**Response:** A key like `ef39510236f064967ac81db786b128d8`, described as a parchment leading to `/decrypt`.

---

### 🔹 Step 3: Decrypt the Message

```bash
curl -X GET "https://workwithus.webminix.com/decrypt?key=ef39510236f064967ac81db786b128d8" \
  -H "User-Agent: Curious_Explorer"
```

**Response:** A poetic narrative describing the "Hall of Symbols" and instructing you to retrieve a hidden phrase from DNS archives.

---

### 🔹 Step 4: Extract Secret from DNS

```bash
dig TXT webminix.com +short
```

**Output:**

```
"Curious_Valut_Secret_Pharse=1319b592dc5f864836f8dfe27989b9afe615d10e4ac6ed01c099715786b9d8d7"
```

📝 Note the typo in `Valut` and `Pharse` — intentional.

---

### 🔹 Step 5: Try to Open the Vault

```bash
curl -X POST "https://workwithus.webminix.com/open" \
  -H "User-Agent: Curious_Explorer" \
  -H "X-Forwarded-Host: webminix.com" \
  -H "X-Requested-With: XMLHttpRequest" \
  -H "Content-Type: application/json" \
  -d '{
    "auth": {
      "type": "vault_passphrase",
      "credentials": {
        "Curious_Valut_Secret_Pharse": "1319b592dc5f864836f8dfe27989b9afe615d10e4ac6ed01c099715786b9d8d7"
      }
    }
  }'
```

**Response:**

```json
{"error":"The Guardian studies your offering but shakes their head. 'This is not the mark of a true seeker. Find the hidden inscription in the archives and return when you carry the true mark.'"}
```

✅ All formatting appears correct — but access is denied, implying a missing transformation or encoding of the hash.

---

## ❌ Where I Got Stuck

Despite following the logical path:

* Tried the direct SHA256 value from DNS
* Tried base64 encoding variations
* Tried guess phrases ("curious\_explorer", "open\_seasame")
* Explored different field/key casing

Still, the Guardian refuses access. This is likely the final twist:

> 🔍 Possibly the hash needs to be **decoded** (pre-image) or transformed into a phrase.

---

## ✅ What This Shows (Skills Demonstrated)

* API request crafting
* Understanding of DNS TXT records
* Logical deduction from narrative clues
* Base64 + hash utility usage
* Persistence and edge-case testing

---

## 📚 Learnings

* Always read error messages as part of the puzzle.
* Typos like `Valut` and `Pharse` are deliberate, not bugs.
* Not every secret is a direct answer — some need transformation.
* Sometimes, a puzzle is designed to **test how you approach being stuck**.

---

## 🙏 Credits

Challenge by [Webminix](https://webminix.com). This walkthrough is intended as a personal learning log and skill showcase — not to spoil the final puzzle.

---

## 🤝 Let’s Connect

If you enjoyed this or want to collaborate:

* 📧 [vivekharsh.work@gmail.com](mailto:vivekharsh.work@gmail.com)
* 🌐 [GitHub](https://github.com/HarshTechStack)
* 🔗 [LinkedIn](https://www.linkedin.com/in/vivekharshcodecraft/)

> “In puzzles — like in engineering — the journey matters more than just the key.”
