CUSTOM DOMAIN SETUP (GitHub Pages)
=================================

This site is hosted with GitHub Pages. Follow these steps to point your own
domain name (example: godmc.com) to your GitHub Pages site.

---------------------------------------------------------------------------
1) CONFIRM GITHUB PAGES IS ENABLED
---------------------------------------------------------------------------

1. Open your repo on GitHub
2. Go to: Settings -> Pages
3. Under "Build and deployment":
   - Source: Deploy from a branch
   - Branch: main (or master, whichever you use)
   - Folder: / (root)  (unless you are using /docs)
4. Make sure your homepage file is named EXACTLY:
   index.html
   and it is located in the folder you selected above.

GitHub will show "Your site is live at ..." on the Pages screen.

---------------------------------------------------------------------------
2) SET THE CUSTOM DOMAIN INSIDE GITHUB
---------------------------------------------------------------------------

1. Go to: Settings -> Pages
2. Find "Custom domain"
3. Enter your domain:
   - godmc.com   (apex/root domain) OR
   - www.godmc.com (subdomain)
4. Click Save

NOTE: GitHub typically creates/updates a file named "CNAME" automatically
in your publishing source after you save the custom domain.

---------------------------------------------------------------------------
3) UPDATE DNS AT YOUR DOMAIN REGISTRAR (MOST IMPORTANT STEP)
---------------------------------------------------------------------------

RECOMMENDED SETUP (BEST): Use BOTH apex + www
This avoids a bunch of common HTTPS/redirect issues.

A) APEX DOMAIN (godmc.com)
Create these A records for "@" pointing to GitHub Pages IP addresses:

Type: A     Name/Host: @     Value: 185.199.108.153
Type: A     Name/Host: @     Value: 185.199.109.153
Type: A     Name/Host: @     Value: 185.199.110.153
Type: A     Name/Host: @     Value: 185.199.111.153

(Some registrars require you to add them as separate entries.)

B) WWW SUBDOMAIN (www.godmc.com)
Create one CNAME record for "www" pointing to your GitHub Pages hostname:

Type: CNAME  Name/Host: www  Value: mrduncle31.github.io

IMPORTANT:
- Use "mrduncle31.github.io" (no repo name at the end).
- Do NOT point the CNAME to the apex via an A record.

ALTERNATE SETUP: Only use a subdomain
If you only want www.godmc.com (and no godmc.com apex):
- In GitHub Pages Custom domain, enter: www.godmc.com
- Create ONLY the CNAME:
  Type: CNAME  Name/Host: www  Value: mrduncle31.github.io

---------------------------------------------------------------------------
4) ENABLE HTTPS
---------------------------------------------------------------------------

After DNS is correct:

1. Go to: Settings -> Pages
2. Turn on: Enforce HTTPS

GitHub will provision a certificate automatically, but it may take a bit
after DNS changes.

---------------------------------------------------------------------------
5) COMMON PROBLEMS + FIXES
---------------------------------------------------------------------------

A) "404 File not found"
- Ensure your repo has index.html in the correct folder (root or /docs)
- Ensure Settings -> Pages is pointing to the correct branch and folder

B) Domain works but HTTPS won't enable
- Double-check the A records and CNAME are exactly correct
- DNS can take time to propagate; try again later after records are set

C) Avoid wildcard DNS (*.godmc.com)
- Wildcards can create security risks and are not recommended for Pages.

D) Domain verification (recommended)
- Verifying your domain in GitHub helps prevent takeover issues if the repo
  or settings change.

---------------------------------------------------------------------------
QUICK CHECKLIST
---------------------------------------------------------------------------

[ ] index.html exists in the folder GitHub Pages is publishing
[ ] Settings -> Pages set to correct branch + folder
[ ] Custom domain saved in Settings -> Pages
[ ] DNS A records set for apex (@) (recommended)
[ ] DNS CNAME set for www -> mrduncle31.github.io (recommended)
[ ] Enforce HTTPS enabled after DNS is valid
