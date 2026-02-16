# GILGAMESH - Game Budget Tracker

A beautiful, privacy-focused Progressive Web App (PWA) for tracking your gaming purchases across all platforms.

## Features

- 📊 **Dashboard Analytics** - Track spending by month and platform
- 🎮 **Multi-Platform Support** - PlayStation, Xbox, Nintendo Switch, PC, and Other
- 💶 **Euro Currency** - Built for European gamers
- 📧 **Gmail Receipt Sync** - Automatically import purchases from PlayStation, Nintendo, Xbox, and Steam receipts
- 💾 **Offline-First** - All data stored locally in your browser (IndexedDB)
- 📱 **Mobile Optimized** - Install as a PWA on your phone
- 🔒 **Privacy Focused** - No backend, no tracking, your data stays on your device

## Gmail Sync Setup

To enable automatic receipt syncing from your Gmail:

1. Follow the detailed instructions in [GMAIL_SETUP.md](GMAIL_SETUP.md)
2. Set up a Google Cloud project and OAuth credentials
3. Enable the Gmail API
4. Update `index.html` with your Client ID
5. Click "Sync Gmail Receipts" on the dashboard

The app will scan your Gmail for purchase receipts from:
- PlayStation Store
- Nintendo eShop
- Xbox/Microsoft Store
- Steam

All processing happens client-side - your emails are never sent to any external server.

## Local Development

Simply open `index.html` in a browser, or use a local web server:

```bash
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Technologies

- Vanilla JavaScript (no frameworks!)
- IndexedDB for local storage
- Google Gmail API with OAuth 2.0
- Service Worker for offline support
- CSS Grid & Flexbox
- Google Fonts (Cinzel + Outfit)

## Privacy

- All purchase data stored locally in your browser
- Gmail OAuth uses read-only scope
- Email parsing happens entirely client-side
- No analytics, no tracking, no external servers
- You own your data

## License

MIT