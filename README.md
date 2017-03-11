# Fix-Missing-Files v0.0.1
Serve replacement files when requests are made for non existent documents i.e. fix 404 errors with a one-size-fits-all patch.

## Notes

- This solution for fixing 404 errors is intended to be used as a quick-fix when other solutions are impractical to apply.
- This solution is not intended to be used to serve 404 error pages though it can be used this way if necessary.

## Instructions

- Download the directory called 'missing'.
- Upload the 'missing' directory to your site's document root (normally under public_html).
- Unpack the uploaded package.
- Make sure 'missing' is directly under public_html
- Copy the .htaccess directives in the 'missing' directory to the .htaccess file immediately under public_html.

## For reference

The .htaccess directives to be added to the root .htaccess file are:

```
## Fix missing image and file requests
## Change each of the two {REQUEST_URI} lines to specify the missing file 404 requests to check against.
## The replacement file(s) to serve should go into a server directory called "missing" located under public_html/
## See https://journalxtra.com/web-development/fix-missing-file-404-requests/
 
## Fix Bad Image Requests
RewriteCond %{REQUEST_FILENAME} !-f
## Add image file types to check against here
RewriteCond %{REQUEST_URI} .(gif|jpe?g|png|bmp|tiff|xcf|psd|ico|svg)$ [NC]
## Specify the file to serve instead
RewriteRule .* /missing/missing.gif [L]
 
## Fix Bad File Requests
RewriteCond %{REQUEST_FILENAME} !-f
## Add file types to check here.
## Put a replacement document in the "missing" directory for each specified file type.
## The replacement document can be an empty text file but with the same extension type as the file it is served in place of.
RewriteCond %{REQUEST_URI} .(css|html?|js|shtml|txt)$ [NC]
RewriteRule .* /missing/missing.%1 [L]
```

The files in the 'missing' directory are:

- missing.gif (1px square)
- missing.css (empty text file)
- missing.htm (empty text file)
- missing.html (empty text file)
- missing.js (empty text file)
- missing.shtml (empty text file)
- missing.txt (empty text file)

## More info

Visit [https://journalxtra.com/web-development/fix-missing-file-404-requests/](https://journalxtra.com/web-development/fix-missing-file-404-requests/)