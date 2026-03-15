═══════════════════════════════════════════════════════════════════
  AMtechiesPRINTER — Complete Setup & Deployment Guide
  Version: 2.0  |  Contact: amtechiesprinter@gmail.com
═══════════════════════════════════════════════════════════════════

📁 FILES IN THIS PACKAGE
─────────────────────────────────────────────────────────────────
  index.html          → Main website (fully updated)
  admin.html          → Admin control panel (private)
  .htaccess           → Apache redirect + security headers
  nginx.conf          → Nginx SSL server configuration
  ssl/
    openssl.cnf       → OpenSSL configuration
    generate-ssl.sh   → Self-signed cert generator script
  README.txt          → This file

═══════════════════════════════════════════════════════════════════
  STEP 1 — ADMIN PANEL LOGIN
═══════════════════════════════════════════════════════════════════

  URL:       https://yoursite.com/admin.html
  Username:  admin   (or: amtechiesprinter@gmail.com)
  Password:  Support@2026

  ⚠  CHANGE YOUR PASSWORD IMMEDIATELY after first login.
     Go to: Admin Panel → Change Password

═══════════════════════════════════════════════════════════════════
  STEP 2 — CONFIGURE TAWK.TO LIVE CHAT
═══════════════════════════════════════════════════════════════════

  Your tawk.to account: amtechiesprinter@gmail.com

  To get your Widget Embed Code:
  1. Login at https://tawk.to
  2. Go to: Administration → Channels → Chat Widget
  3. Click the "JavaScript" tab
  4. Your embed code looks like:
       s1.src='https://embed.tawk.to/YOUR_PROPERTY_ID/YOUR_WIDGET_ID';
  5. Copy YOUR_PROPERTY_ID and YOUR_WIDGET_ID
  6. Open Admin Panel → Tawk.to Chat
  7. Enter the IDs and click Save
  8. Copy the generated embed code
  9. In index.html, find this comment:
       <!--Start of Tawk.to Script-->
     Replace that entire block with your new embed code.

═══════════════════════════════════════════════════════════════════
  STEP 3 — ACTIVATE CONTACT FORM EMAIL
═══════════════════════════════════════════════════════════════════

  FormSubmit.co is pre-configured for amtechiesprinter@gmail.com

  To activate email notifications:
  1. Deploy the site to your server
  2. Submit any test contact form
  3. Check amtechiesprinter@gmail.com for a confirmation email
  4. Click the activation link in that email
  5. ✓ All future form submissions will email you automatically

  Email fields in every submission:
  - Full Name
  - Phone Number
  - Email Address
  - Address
  - Printer Brand & Model
  - Issue Type
  - Problem Description
  - Preferred Contact Method

═══════════════════════════════════════════════════════════════════
  STEP 4 — UPDATE TFN & EMAIL VIA ADMIN PANEL
═══════════════════════════════════════════════════════════════════

  Open: https://yoursite.com/admin.html

  → To change Toll Free Number:
    Admin Panel → TFN & Contact → Update and Save

  → To change Support Email:
    Admin Panel → Email Settings → Update and Save

  Changes apply instantly on the website via localStorage sync.

  NOTE: Admin panel changes use browser localStorage.
  They affect the site for all visitors on the SAME hosting server.
  For permanent HTML-level changes, edit index.html directly.

═══════════════════════════════════════════════════════════════════
  STEP 5 — SSL CERTIFICATE SETUP
═══════════════════════════════════════════════════════════════════

  ─── OPTION A: Let's Encrypt (FREE — Recommended) ──────────────

  Best for: Live servers with a domain name

    # Install Certbot
    sudo apt update
    sudo apt install certbot python3-certbot-nginx

    # Get free SSL certificate
    sudo certbot --nginx -d amtechiesprinter.com -d www.amtechiesprinter.com

    # Auto-renewal (runs twice daily)
    sudo systemctl enable certbot.timer

  ─── OPTION B: Self-Signed Certificate (Testing Only) ─────────

  For local/testing use (browsers will show security warning):

    cd ssl/
    chmod +x generate-ssl.sh
    ./generate-ssl.sh

  This creates:
    ssl/server.key     → Private Key  ⚠ KEEP SECRET
    ssl/server.csr     → CSR
    ssl/server.crt     → Certificate
    ssl/server.pem     → PEM Bundle
    ssl/dhparam.pem    → DH Parameters

  ─── OPTION C: Paid SSL Certificate ───────────────────────────

  Buy from: Namecheap, Comodo, DigiCert
  After purchase:
  1. Generate CSR using ssl/openssl.cnf
  2. Submit CSR to your CA
  3. Download certificate files
  4. Update nginx.conf paths

═══════════════════════════════════════════════════════════════════
  STEP 6 — DEPLOY TO SERVER (Nginx)
═══════════════════════════════════════════════════════════════════

  1. Upload all files to: /var/www/amtechiesprinter/
     (Do NOT upload ssl/ folder to public web root)

  2. Copy nginx config:
     sudo cp nginx.conf /etc/nginx/sites-available/amtechiesprinter.com

  3. Enable the site:
     sudo ln -s /etc/nginx/sites-available/amtechiesprinter.com \
                /etc/nginx/sites-enabled/

  4. Test config:
     sudo nginx -t

  5. Reload Nginx:
     sudo systemctl reload nginx

═══════════════════════════════════════════════════════════════════
  STEP 7 — DEPLOY TO SERVER (Apache / cPanel)
═══════════════════════════════════════════════════════════════════

  1. Upload these files to your public_html folder:
       index.html
       admin.html
       .htaccess

  2. The .htaccess auto-redirects HTTP → HTTPS

  3. For SSL: Use your cPanel's "Let's Encrypt SSL" tool
     (Most cPanel hosts have this built-in for free)

═══════════════════════════════════════════════════════════════════
  STEP 8 — GOOGLE ADS VERIFICATION
═══════════════════════════════════════════════════════════════════

  1. Go to: https://search.google.com/search-console
  2. Add property: https://amtechiesprinter.com
  3. Choose "HTML tag" verification method
  4. Copy the content= value
  5. In index.html, find this line:
     <meta name="google-site-verification" content="YOUR_GOOGLE_VERIFICATION_CODE_HERE" />
  6. Replace YOUR_GOOGLE_VERIFICATION_CODE_HERE with your code
  7. Re-upload index.html
  8. Click Verify in Search Console

═══════════════════════════════════════════════════════════════════
  SECURITY NOTES
═══════════════════════════════════════════════════════════════════

  ⚠  IMPORTANT:
  • Change the admin password immediately (default: Support@2026)
  • Rename admin.html to something less obvious in production
    e.g.: amtprinter-control-9x2.html
  • Do NOT share admin.html URL publicly
  • Keep server.key file permissions at 600 (never 644)
  • Enable 2FA on your Gmail (amtechiesprinter@gmail.com)
  • Enable 2FA on your Tawk.to account
  • Backup your site files weekly

═══════════════════════════════════════════════════════════════════
  SUPPORT
═══════════════════════════════════════════════════════════════════

  Website Contact : amtechiesprinter@gmail.com
  Company         : AMtechiesPRINTER
  Admin Panel URL : /admin.html

═══════════════════════════════════════════════════════════════════
