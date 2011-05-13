sf2github README
================

`sf2github` is a Python program that reads an XML export from a SourceForge project and pushes this data to GitHub via its REST API.

The script is currently very incomplete and barely tested. If it works for you, great; if not, fix it up and send me a pull request! Currently, only migration of tracker issues is partly implemented, and there's no error handling.

Also note that the GitHub API is quite slow, taking about 5 seconds per request on my machine and internet connection. Migration of a large project will take a while.

Issue migration
---------------

What works (for me):

* SF tracker issues become GitHub tracker issues.
* Comments on SF become comments in GitHub.
* Groups and categories on SF both become labels on GitHub.
* Issues with a status that is exactly the text "Closed" or "Deleted" will be closed on GitHub.

Limitations:

* Only a single tracker is supported, though this could be easily fixed.
* All issues and comments will be owned by the project's owner on GitHub, but mention the SF username of the original submitter.
* There's some rubbish in the comment text sometimes (Logged In, user_id, Originator) but this is in the SF XML export.
* There are encoding errors in the SF export of (at least) comments. Non-ASCII characters are encoded with UTF-8, then decoded (interpreted) as CP1252, and those code points gets encoded as XML entities. The script does not work around this. See also http://stackoverflow.com/questions/5291081/how-did-sourceforge-maim-this-unicode-character

Code migration
--------------

This script doesn't help you to migrate code from SF's Subversion to GitHub. However, I found the following page helpful in doing that: http://help.github.com/svn-importing/

Usage
-----

From SourceForge, you need to export the tracker data in XML. Read [here](https://sourceforge.net/apps/trac/sourceforge/wiki/XML%20export) for instructions.

Run the `issues.py` script and it will print further instructions. Basically, if your SF XML export is in `foo.xml`, your GitHub username is `john` and your repository is `bar`:

    ./issues.py foo.xml john/bar

License
-------

This software is in the public domain. I accept no responsibility for any damage resulting from it. Use at your own risk.

