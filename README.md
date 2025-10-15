# 🚀 DAX Expert Assistant - Firebase Hosting Edition

**A Claude AI-powered DAX solution assistant website ready for Firebase Hosting deployment**

[![Firebase](https://img.shields.io/badge/Firebase-Hosting-orange.svg)](https://firebase.google.com/)
[![Claude AI](https://img.shields.io/badge/Powered%20by-Claude%20AI-blue.svg)](https://www.anthropic.com/claude)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Files in This Repository](#files-in-this-repository)
- [Prerequisites](#prerequisites)
- [Firebase Setup & Deployment Instructions](#firebase-setup--deployment-instructions)
- [Local Testing](#local-testing)
- [Backend Integration](#backend-integration)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## 🎯 Overview

This repository contains a fully functional frontend application for a DAX (Data Analysis Expressions) Expert Assistant powered by Claude AI. The application features an intuitive chat interface where users can ask questions about DAX formulas, Power BI, and get AI-powered responses.

## ✨ Features

- **💬 Interactive Chat Interface**: Clean, modern chat UI for seamless interaction
- **🤖 Claude AI Integration Ready**: Prepared for backend API connection
- **📱 Responsive Design**: Works beautifully on desktop and mobile devices
- **🎨 Beautiful UI**: Gradient background and polished design elements
- **⚡ Fast Performance**: Lightweight single-page application
- **🔧 Firebase Ready**: Pre-configured for Firebase Hosting deployment

## 📁 Files in This Repository

```
dax-expert-assistant-firebase/
├── index.html       # Main application file with HTML, CSS, and JavaScript
├── firebase.json    # Firebase Hosting configuration
├── .firebaserc      # Firebase project configuration (template)
└── README.md        # This file
```

## 📦 Prerequisites

Before deploying to Firebase Hosting, ensure you have:

1. **Node.js and npm** installed on your system
   - Download from: https://nodejs.org/
   - Verify installation: `node --version` and `npm --version`

2. **A Firebase Account**
   - Sign up at: https://firebase.google.com/

3. **Firebase CLI** installed globally
   ```bash
   npm install -g firebase-tools
   ```

## 🚀 Firebase Setup & Deployment Instructions

### Step 1: Clone This Repository

```bash
git clone https://github.com/BhanuprakashAvadutha/dax-expert-assistant-firebase.git
cd dax-expert-assistant-firebase
```

### Step 2: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or "Create a project"
3. Enter a project name (e.g., "dax-expert-assistant")
4. Follow the setup wizard (you can disable Google Analytics if not needed)
5. Click "Create project"

### Step 3: Login to Firebase CLI

```bash
firebase login
```

This will open a browser window for you to authenticate with your Google account.

### Step 4: Initialize Firebase in Your Project

```bash
firebase init hosting
```

During initialization:
- **Select project**: Choose the Firebase project you created in Step 2
- **What do you want to use as your public directory?** Type: `.` (current directory)
- **Configure as a single-page app?** Type: `y` (yes)
- **Set up automatic builds with GitHub?** Type: `N` (no, unless you want CI/CD)
- **Overwrite existing files?** Type: `N` (no) - keep your existing files

### Step 5: Update .firebaserc File

Open `.firebaserc` and replace `your-firebase-project-id` with your actual Firebase project ID:

```json
{
  "projects": {
    "default": "your-actual-project-id"
  }
}
```

You can find your project ID in the Firebase Console under Project Settings.

### Step 6: Deploy to Firebase Hosting

```bash
firebase deploy --only hosting
```

After successful deployment, you'll see output like:

```
✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/your-project-id/overview
Hosting URL: https://your-project-id.web.app
```

### Step 7: Access Your Deployed Website

Your DAX Expert Assistant is now live! Visit the Hosting URL provided in the deployment output.

## 🧪 Local Testing

Before deploying, you can test your application locally:

### Method 1: Using Firebase Emulator

```bash
firebase serve
```

Then open http://localhost:5000 in your browser.

### Method 2: Using Python's Simple HTTP Server

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

Then open http://localhost:8000 in your browser.

### Method 3: Using VS Code Live Server

1. Install the "Live Server" extension in VS Code
2. Right-click on `index.html`
3. Select "Open with Live Server"

## 🔗 Backend Integration

The current `index.html` includes a placeholder response. To connect with Claude AI:

### Option 1: Firebase Cloud Functions

1. Create a Firebase Cloud Function to handle API requests:

```javascript
const functions = require('firebase-functions');
const Anthropic = require('@anthropic-ai/sdk');

exports.chat = functions.https.onRequest(async (req, res) => {
  // Enable CORS
  res.set('Access-Control-Allow-Origin', '*');
  
  if (req.method === 'OPTIONS') {
    res.set('Access-Control-Allow-Methods', 'POST');
    res.set('Access-Control-Allow-Headers', 'Content-Type');
    res.status(204).send('');
    return;
  }

  const anthropic = new Anthropic({
    apiKey: functions.config().anthropic.key,
  });

  const { query } = req.body;

  const message = await anthropic.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 1024,
    messages: [{ role: 'user', content: query }],
  });

  res.json({ response: message.content[0].text });
});
```

2. Update the fetch URL in `index.html` to your Cloud Function URL

### Option 2: External Backend Service

You can use any backend service (Node.js, Python, etc.) that integrates with Claude AI. Just update the fetch URL in the `sendMessage()` function.

## ⚙️ Configuration

### Customizing firebase.json

The `firebase.json` file includes:
- **Public directory**: Set to current directory (`.`)
- **Single-page app**: Rewrites all routes to `index.html`
- **Cache headers**: Optimized caching for static assets

You can modify these settings based on your needs.

### Customizing the UI

The entire application is contained in `index.html`. You can customize:
- **Colors**: Modify the CSS gradient and color values
- **Fonts**: Change the font-family in the CSS
- **Content**: Update text, titles, and example queries
- **Functionality**: Extend the JavaScript for additional features

## 🐛 Troubleshooting

### Issue: "Firebase not found" error
**Solution**: Make sure Firebase CLI is installed globally:
```bash
npm install -g firebase-tools
```

### Issue: Permission denied during deployment
**Solution**: Re-authenticate with Firebase:
```bash
firebase logout
firebase login
```

### Issue: Changes not reflecting after deployment
**Solution**: Clear your browser cache or use an incognito window. Also ensure you ran:
```bash
firebase deploy --only hosting
```

### Issue: 404 errors on refresh
**Solution**: Ensure your `firebase.json` has the rewrite rule for single-page apps (already included in this repo).

## 📚 Additional Resources

- [Firebase Hosting Documentation](https://firebase.google.com/docs/hosting)
- [Firebase CLI Reference](https://firebase.google.com/docs/cli)
- [Claude AI Documentation](https://docs.anthropic.com/)
- [DAX Reference](https://dax.guide/)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- Built with ❤️ using Claude AI by Anthropic
- Hosted on Firebase Hosting by Google
- Designed for the Power BI and DAX community

---

**Need Help?** Open an issue in this repository or contact the maintainer.

**Ready to Deploy?** Follow the steps above and get your DAX Expert Assistant live in minutes! 🚀
