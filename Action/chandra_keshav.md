Since you want to handle redirects from the old structure https://docs.mosip.io/inji/*/* to the new structure https://docs.inji.io/*/*, you can use a global redirection method on the old site (docs.mosip.io/inji) rather than modifying individual pages.
GitBook doesn’t allow server-side configurations like .htaccess, but you can still use JavaScript for a dynamic redirect based on the current URL. Here’s how you can achieve this:
# 1. Add a Global JavaScript Redirection for the Entire Inji Section
You’ll need to place a universal redirect script on all pages under https://docs.mosip.io/inji. This script will dynamically map any old URLs (with the inji prefix) to the new domain structure (docs.inji.io).
Code for Global Redirect:
Modify the index.html file in the root folder of docs.mosip.io/inji (or wherever GitBook serves your main entry point for the Inji documentation) and include this JavaScript:
html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript">
        // Get the current URL path after /inji
        var currentPath = window.location.pathname.replace("/inji", "");
        
        // Construct the new URL on docs.inji.io with the same path
        var newUrl = "https://docs.inji.io" + currentPath + window.location.search + window.location.hash;
        
        // Redirect to the new URL
        window.location.href = newUrl;
    </script>
    <title>Redirecting...</title>
</head>
<body>
    <p>If you are not redirected automatically, follow this <a href="https://docs.inji.io">link</a>.</p>
</body>
</html>
```

# 2. Where to Add the Redirection Code:
Add this index.html file to the root of the inji directory in your docs.mosip.io GitBook project.
This script will dynamically capture any URL under docs.mosip.io/inji/*/* and redirect users to the corresponding path on docs.inji.io/*/*.

## Example:
A request to https://docs.mosip.io/inji/guide/getting-started will be automatically redirected to https://docs.inji.io/guide/getting-started.
The script captures the part after /inji/ and appends it to the docs.inji.io domain.
# 3. Deploy and Test:
Once you have added this redirect logic in the index.html of the Inji folder, push it to GitBook and redeploy the documentation.
Test by visiting various old URLs (e.g., https://docs.mosip.io/inji/guide/getting-started) to ensure they redirect correctly to the new domain (https://docs.inji.io/guide/getting-started).
Notes:
If you have multiple entry points under https://docs.mosip.io/inji/*/*, you can replicate this index.html file in those subdirectories as well.
GitBook’s static site setup may require redeploying after every change. Ensure your GitBook configuration reflects these changes and that it rebuilds properly.
By implementing this, your entire docs.mosip.io/inji/*/* structure will seamlessly redirect to docs.inji.io/*/*, preserving the link structure for old URLs.