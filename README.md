# Fix-Missing-Files v0.0.2
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
## Change each of the {REQUEST_URI} lines in each directive set to specify the missing file 404 requests to check against.
## The replacement file(s) to serve should go into a server directory called "missing" located under public_html/
## Image formats go into the Image Set. No file required to be added to the 'missing' directory
## Other formats go into the File Set. Place an empty text file with correct extension into the 'missing' directory
## See https://journalxtra.com/web-development/fix-missing-file-404-requests/
 
## Image Set: Fix Bad Image Requests
RewriteCond %{REQUEST_FILENAME} !-f
## Ignore any real files (404s will not occur if the file actually exists)
## Add image file types to check against here
RewriteCond %{REQUEST_URI} .(gif|jpe?g|png|bmp|tiff|xcf|psd|ico)$ [NC]
## Specify the file to serve instead
RewriteRule .* /missing/missing.gif [L]
 
## File Set: Fix Bad File Requests
## Ignore specific virtual file(s)
RewriteCond %{REQUEST_URI} !^/robots.txt/? [NC]
## Ignore any real files (404s will not occur if the file actually exists)
RewriteCond %{REQUEST_FILENAME} !-f
## Add file types to check here.
## Put a replacement document in the "missing" directory for each specified file type.
## The replacement document can be an empty text file but with the same extension type as the file it is served in place of.
RewriteCond %{REQUEST_URI} .(css|html?|js|php|shtml|svg|txt)$ [NC]
RewriteRule .* /missing/missing.%1 [L]
```

## Files in the Missing directory

These are the files in the 'missing' directory. These are served when 404s are encountered. These are empty files. If you wish you can replace them with non-empty files to serve when missing files are encounted but I advise against it.

- missing.gif (1px square)
- missing.css (empty text file)
- missing.htm (empty text file)
- missing.html (empty text file)
- missing.js (empty text file)
- missing.php (empty text file)
- missing.shtml (empty text file)
- missing.svg (empty text file)
- missing.txt (empty text file)

# Warnings and Notes

If you use a CMS that creates virtual files be careful not to add those virtual file formats to the list of formats to check against or at least whitelist specific virtual files with a directive instructing the server to ignore the files (see comments within the File Set directives for an example of whitelisting).

## WordPress Virtual File Formats

These are virtual files and file formats encountered by me:

- xml (created by Jetpack and SEO plugins)
- robots.txt (created by SEO plugins)

# Changelog


0.0.2 - 13th March 2017

- Minor readme.md changes
- Moved svg to File Set from Image Set

0.0.1 - 10th March 2017

- First public release

# More info

Visit [https://journalxtra.com/web-development/fix-missing-file-404-requests/](https://journalxtra.com/web-development/fix-missing-file-404-requests/)
