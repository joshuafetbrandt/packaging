# packaging
This is a high-level set of notes on packaging code for distribution via PyPi. This set of notes is very different from everything else you will find online. 

### Directions for Uploading to PyPi

These directions assume you have already set up an account with TestPyPi and PyPi. If you haven't already done this, start by setting up these accounts. Make sure you set up the account using a token. Tokens are an alternate way to authorize a new upload to PyPi. It is possible to do this with your username and password, but that initiates plaintext transfer of credentials which is dangerous for your distribution long-term. If you go the token route like I recommend, YOU MUST KEEP A COPY OF THE TOKEN. The token is only shown once, so it is critically important that you take a copy of it immediately. You can reset tokens, but that is a lot of work. 

1. Make sure twine is installed. Try `pip install twine`.
2. Change your directory into the main package folder.
3. Run `python setup.py sdist` to (re)build the package.
4. This step is optional, but recommended. Make sure things are okay with a test upload to TestPyPi. Run `twine upload --repository testpypi dist/*`. 
5. If things check out, run `twine upload dist/*`.
6. When prompted for the user name, use `__token__`. 
7. When prompted for the password, use the token generated upon registering with PyPi.

### Issues with Uploading to PyPi

Versioning is critically important with PyPi. It took me a long time to figure out that I needed to update VERSION in the setup.py file every time I did an upload. A corollary to this observation is that you cannot update a current version of a package; this means an update, for any reason, requires a new version to be uploaded. 

Related to this problem was the dist folder in the package. After you (re)build the package, the dist folder will update to contain the packagename-version.tar.gz for each and every current or prior distribution. For whatever reason, sometimes this folder will get out of sync and prevent the package from working with the `twine` upload process given above. The only way I found to fix this out-of-sync-ness was to clear the dist folder and rebuild the package. Both of these are also true for TestPyPi. 

### Resources

https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools

https://www.freecodecamp.org/news/build-your-first-python-package/
