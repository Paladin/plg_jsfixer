Javascript Fixer System Plugin
==============================

This Joomla plugin enables substituting a Javascript library of your choice for the libraries shipped with Joomla. It replaces the jQuery library, the jQuery migration library and the Bootstrap javascript library with ones of your own choosing. This way you can choose to load jQuery/Bootstrap from a common CDN (taking advantage of using a common source, and thus having the library already in your user's cache) or enabling you to update the older libraries that have shipped with Joomla.

Installation
------------

Zip the root directory of this repo. I usually use

```
zip -r -FS -x *.DS_STORE
```

inorder to filter out the Mac desktop files in the directories, just to keep the volume down.

After zipping the files, they can be installed just like any other Joomla plugin. Then go edit the plugin from the administration section to set up the libraries to replace.

Which Way Do I Go?
------------------

There are separate  on/off toggles for jQuery and Bootstrap. Once one of the toggles is switched on, you can type in the URL of the library you want to use.

**Note:** You can load from either https or http by starting the URL *after* the scheme, like this:

```
//code.jquery.com/jquery-1.12.4.min.js
```

That will let your user load jQuery from the main jQuery CDN using whatever scheme (http or https) they are talking to the rest of your site.

How Do I Know You're You?
-------------------------

Whenever you're loading sites from a server not in your control, there's always the risk that an attacker has penetrated the CDN and injected some malicious code into every download. [Subresource Integrity checking](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) was invented to mitigate that risk.

Browsers that support this security feature are given a hash they can check to ensure they received the file they expected to receive. jQuery and Bootstrap both make those hashes available to you along with their CDN links. Enter both the URL and the SRI hash in fields provided for that purpose.

I'm Not Your Mother, But I Still Clean Up After You
---------------------------------------------------

Once you start playing with other versions of jQuery, you will notice some errors getting thrown by both the tootip and popover javascript code. The reason for that is the routines in core don't check before calling, and when nothing uses tooltips ot popovers, the function isn't there to be called.

The other function of this plugin (where the "fixer" part comes from) is that it includes cleaned-up versions of those two routines which it overrides the existing core routines with, eliminating the tendency to litter your user's browser consoles with error messages (the errors don't hurt anything by being there, except perhaps your pride).
