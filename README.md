# cryptpad-ec2-deploy

This guide helps you install and launch CryptPad on an AWS EC2 instance using the official GitHub repository.

---

## ✅ Step 1: Connect to EC2

```bash
ssh -i <your-key.pem> ubuntu@<your-ec2-ip>
```

---

## ✅ Step 2: Install Dependencies

```bash
sudo apt update && sudo apt install -y git curl nginx build-essential

# Install Node.js (LTS)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

---

## ✅ Step 3: Clone CryptPad and Install

```bash
git clone -b 2025.3.0 --depth 1 https://github.com/cryptpad/cryptpad.git cryptpad
cd cryptpad
npm ci
npm run install:components
```

---

## ✅ Step 4: Configure CryptPad

```bash
cp config/config.example.js config/config.js
nano config/config.js
```

Replace the lines below with your actual EC2 DNS or public IP:

```js
httpUnsafeOrigin: 'http://<your-ec2-dns>:3000',
httpSafeOrigin: 'http://<your-ec2-dns>:3000',
httpAddress: '0.0.0.0',
```

---

## ✅ Step 5: Start Server and Setup Admin

```bash
node server.js
```

Then open the URL printed in the terminal in your browser:

```
http://<your-ec2-dns>:3000/install/#<token>
```

Follow the setup wizard to create your admin account and configure the instance.