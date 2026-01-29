
---

# 📑 Tab Saver (Chrome Extension)

A lightweight and efficient Google Chrome extension designed to help you save URLs, organize leads, and manage your browsing tabs instantly. This tool leverages the **Chrome Tabs API** and **Local Storage** to ensure your data persists even after you close the browser.

## 📖 Overview

This extension solves the problem of losing important research tabs or leads. Instead of bookmarking every single page and cluttering your browser bar, you can simply click "Save Tab" to store the URL in a neat list. It also allows for manual input of URLs and features a "Double-Click to Delete" safety mechanism to clear your list.

## 📸 Screenshots
![Platform Preview](screenshots/tabsaver1.png)
![Inputting Tab](screenshots/tabsaver2.png)
![Saving the tab](screenshots/tabsaver3.png) 

## ✨ Key Features

* **Save Current Tab:** Instantly grabs the URL of the active tab using `chrome.tabs.query` and adds it to your list.
* **Manual Input:** Type or paste any URL into the input field to save it manually.
* **Data Persistence:** Uses `localStorage` to save your leads as a JSON string. Your list remains intact even if you refresh or close the extension.
* **Double-Click to Delete:** A safety feature on the "Delete All" button prevents accidental deletion of your saved data.
* **Direct Links:** Saved items are rendered as clickable `<a>` tags that open in a new tab (`target='_blank'`).

## 🛠️ Tech Stack

* **Core:** HTML5, CSS3, JavaScript (ES6)
* **Chrome API:** `chrome.tabs` permission (Manifest V3)
* **Storage:** Browser LocalStorage API

## 🚀 Installation & Setup

Since this is a custom extension, you will need to load it into Chrome in "Developer Mode".

1. **Clone the repository:**
```bash
git clone https://github.com/Otormin/TabSavingChromeExtention.git

```


2. **Open Chrome Extensions:**
Type `chrome://extensions/` in your address bar.
3. **Enable Developer Mode:**
Toggle the switch in the top-right corner to **ON**.
4. **Load Unpacked:**
Click the **"Load unpacked"** button in the top-left corner.
5. **Select Folder:**
Select the folder where you cloned this repository.
6. **Pin & Use:**
Pin the extension to your toolbar and start saving tabs!

## 📂 Code Logic

The extension relies on a `render()` function that dynamically updates the DOM based on the `myLeads` array.

```javascript
// Saving the current tab
tabBtn.addEventListener("click", function(){
    chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
        myLeads.push(tabs[0].url) // Grabs the URL
        localStorage.setItem("myLeads", JSON.stringify(myLeads)) // Saves to Storage
        render(myLeads) // Updates UI
    })
})

```

## 📜 Manifest Permissions

This project uses **Manifest V3**.

* `"permissions": ["tabs"]`: This is strictly required to read the URL of the currently active browser tab when you click the "Save Tab" button.