Here's a clean and professional **README.md** for your **Shake AI** Chrome extension. 🚀  

---

# 🌀 Shake AI - Chrome Extension  
*A lightweight AI-powered Chrome extension using Vue 3, Vite, and Tailwind CSS.*  

## 📌 Features  
✅ **Google Prompt API Integration** - Uses `promptStreaming()` for real-time AI responses  
✅ **Vue 3 & Vite** - Fast and modern frontend framework  
✅ **Tailwind CSS** - Sleek and responsive UI  
✅ **Minimalist & User-Friendly**  

---

## 📂 Project Structure  
```
shake-ai/
│── manifest.json          # Chrome Extension Manifest V3  
│── index.html             # Main extension UI  
│── src/  
│   ├── main.js            # Vue App Entry  
│   ├── App.vue            # Main Component  
│   ├── index.css          # Tailwind Styles  
│── public/  
│   ├── icon.png           # Extension Icon  
│── package.json           # Project Dependencies  
│── tailwind.config.js     # Tailwind Configuration  
│── vite.config.js         # Vite Configuration  
│── .gitignore             # Git Ignore Rules  
│── README.md              # Project Documentation  
```

---

## 🛠 Installation  

### 1️⃣ Install Dependencies  
```sh
npm install
```

### 2️⃣ Start Development Server  
```sh
npm run dev
```
> **Note:** The Chrome extension **cannot** be directly previewed in a browser. You need to load it into Chrome manually.  

### 3️⃣ Build for Production  
```sh
npm run build
```
This will generate a `dist/` folder with the built extension.

---

## 🚀 Load the Extension in Chrome  

1. Open **Chrome** and go to `chrome://extensions/`  
2. Enable **Developer Mode** (toggle in the top-right corner)  
3. Click **Load Unpacked**  
4. Select the **`dist/`** folder  
5. Click on the extension icon in the Chrome toolbar and start chatting! 🤖  

---

## 📝 Usage  

1️⃣ **Enter a system prompt** to set the AI’s behavior  
2️⃣ **Click "Start Session"** to initialize the AI session  
3️⃣ **Type a question** and hit **Send**  
4️⃣ **See real-time AI responses** with `promptStreaming()`  

---

## 📜 Manifest (V3)  
The extension uses **Manifest V3** and requires **AI permissions**:  
```json
{
  "manifest_version": 3,
  "name": "Shake AI",
  "version": "1.0",
  "permissions": ["aiLanguageModelOriginTrial"],
  "host_permissions": ["https://*/*"],
  "action": {
    "default_popup": "index.html"
  }
}
```

---

## 🤝 Contributing  
Got ideas or improvements? Feel free to open a **Pull Request**! 🚀  

---

## 📃 License  
This project is licensed under the **MIT License**.  

---

Now you're all set with a **polished README** for your project! 🎯 Let me know if you need any changes. 🚀🔥