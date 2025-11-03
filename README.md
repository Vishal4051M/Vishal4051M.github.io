# 🌐 ZapShare Website - zapshare.me

This is the standalone website for ZapShare that allows users to send files to devices by entering an 8-digit code.

## Features

✅ **Code-based Connection** - Enter an 8-digit code to connect to a device  
✅ **Automatic IP Resolution** - Converts base-36 codes to IP addresses  
✅ **Connection Testing** - Verifies device availability before redirecting  
✅ **Beautiful UI** - Apple-like design matching the ZapShare app theme  
✅ **Fully Responsive** - Works on desktop, tablet, and mobile  
✅ **No Backend Required** - Pure HTML/CSS/JavaScript

## How It Works

1. User opens zapshare.me
2. Enters the 8-digit code (e.g., `C0A80164`) shown in the ZapShare app
3. JavaScript decodes the code to an IP address (e.g., `192.168.1.100`)
4. Tests if the device is reachable on port 8090
5. Redirects to `http://<ip>:8090` to upload files

## Code Conversion Logic

The 8-digit code is a base-36 representation of the IP address:

```javascript
// IP to Code (done in the app)
function ipToCode(ip) {
  const parts = ip.split('.').map(Number);
  const num = (parts[0] << 24) | (parts[1] << 16) | (parts[2] << 8) | parts[3];
  return num.toString(36).toUpperCase().padStart(8, '0');
}

// Code to IP (done on website)
function codeToIp(code) {
  const num = parseInt(code, 36);
  return `${(num >> 24) & 0xFF}.${(num >> 16) & 0xFF}.${(num >> 8) & 0xFF}.${num & 0xFF}`;
}
```

### Examples:
| IP Address | 8-Digit Code |
|-----------|-------------|
| 192.168.1.1 | C0A80101 |
| 192.168.1.100 | C0A80164 |
| 10.0.0.5 | 0A000005 |

## Local Testing

You can test the website locally using any HTTP server:

### Using Python (recommended):
```bash
cd zapshare-website
python -m http.server 8080
```

Then open: http://localhost:8080

### Using Node.js:
```bash
npm install -g http-server
cd zapshare-website
http-server -p 8080
```

### Using PHP:
```bash
cd zapshare-website
php -S localhost:8080
```

## Deployment

### Option 1: GitHub Pages (Free)

1. Create a GitHub repository
2. Upload `index.html` to the repository
3. Go to Settings → Pages
4. Select source: `main` branch
5. Your site will be live at `https://yourusername.github.io/repo-name`

### Option 2: Netlify (Free)

1. Sign up at [netlify.com](https://netlify.com)
2. Drag and drop the `zapshare-website` folder
3. Your site will be live instantly with a custom domain option

### Option 3: Vercel (Free)

1. Sign up at [vercel.com](https://vercel.com)
2. Import from GitHub or upload files
3. Deploy with one click

### Option 4: Custom Domain

If you own `zapshare.me`:

1. Deploy using any of the above services
2. Point your domain's DNS to the deployment
3. Configure SSL certificate (usually automatic)

## File Structure

```
zapshare-website/
├── index.html          # Main landing page with code input
└── README.md          # This file
```

## Browser Compatibility

✅ Chrome/Edge (latest)  
✅ Firefox (latest)  
✅ Safari (latest)  
✅ Mobile browsers  

## Security Notes

- All communication happens on local network (no data leaves your network)
- The website itself doesn't handle file transfers
- It only redirects to the device's local IP address
- CORS and same-network requirements provide security

## Customization

You can easily customize:
- Colors (search for `#FFD600` to change yellow theme)
- Logo emoji (change `⚡` to your preference)
- Text and messaging
- Animations and transitions

## Future Enhancements

Potential features to add:
- [ ] QR code scanning for easy code entry
- [ ] Recent connections history (stored locally)
- [ ] Dark/light theme toggle
- [ ] Multi-language support
- [ ] Progressive Web App (PWA) support

## Support

For issues or questions:
- GitHub Issues: [Create an issue](https://github.com/Vishal4051M/ZapShare/issues)
- Email: support@zapshare.me (if domain is active)

## License

Same license as the main ZapShare project.

---

Made with ⚡ by the ZapShare Team

## Manual fallback link

If the site cannot automatically open or fetch files (for example due to browser mixed-content blocking or network routing), the UI will display a direct link constructed from the decoded IP and port. You can click the link, copy it to the clipboard, or open it in a new tab.

- Send (open) port used by the site: 8090
- Receive (list/file) port used by the site: 8080

Example fallback link: http://192.168.1.100:8080
