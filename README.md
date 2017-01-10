# Remark.js (markdown-to-slides)

### Instructions to install

To work on atom:

* Install remark: atom packages-> remark (from terminal: apm install linter-remark)
* Install slide preview
* We need to Install markdown-to-slides, but before we need to be sure we have the correct version of nodejs in our mac. Install home brew and be sure you do not have a previous version, other wise follow (from https://gist.github.com/DanHerbert/9520689)
	 ```bash
rm -rf /usr/local/lib/node_modules
brew uninstall node
brew install node --without-npm
echo prefix=~/.npm-packages >> ~/.npmrc
curl -L https://www.npmjs.com/install.sh | sh
```
Node and npm should be correctly installed at this point. The final step is to add ``~/.npm-packages/bin ``to your PATH so npm and global npm packages are usable. To do this, add the following line to your ``~/.bash_profile``:

export ``PATH="$HOME/.npm-packages/bin:$PATH"``
Now you can re-install any global npm packages you need without any problems.

To test out your Node and npm install, try installing Grunt
``npm install -g grunt-cl``.

* Now we install the markdown-to-slides: ``npm install markdown-to-slides -g``.
* Then, in order to avoid the problem: env: node``\r``: No such file or directory we have to edit the script in the markdown-to-slide directory index.js. There is a problem with newlines in your script. Make sure that ``#! /usr/bin/env node`` is followed by ``\n ``(unix style) instead of ``\r\n`` (windows/dos style). To fix that, use the ``tr`` command to remove ``\r``'s from your file. Therefore we go to the ``cd ../lib/node_modules/markdown-to-slides``. Once there, we can look for the index.js and make a copy before manipulating the file:

```bash
$ ls
LICENSE README.md index.js lib node_modules package.json template test

starignus@ariadnasmacbook ~/.npm-packages/lib/node_modules/markdown-to-slides
$ cp index.js index_original.js 

starignus@ariadnasmacbook ~/.npm-packages/lib/node_modules/markdown-to-slides
$ ls
LICENSE index.js lib package.json test
README.md index_original.js node_modules template
```

Now, to remove the ``\r``:

```
$ cat index.js | tr -d '\r' > index_2.js

mymack@macbook
~/.npm-packages/lib/node_modules/markdown-to-slides
$ cp index_2.js index.js 

mymack@macbook~/.npm-packages/lib/node_modules/markdown-to-slides$ rm index_2.js
```

* Now you can run the markdown-to-slide:
```bash
mymack@macbook ~/Documents/HorizonCourse/Extra_info
$ markdown-to-slides Test.md -o slideshow.html
10:42:53 AM: "Test.md" written in "slideshow.html"```

or using an optional css:

```bash
markdown-to-slides Test_as_slides.md -o slideshow_asslides.html -s remark-template-basic.css
```

## Links

* About the syntax and styling look at: https://github.com/gnab/remark/wiki/Markdown;
* remark.js https://github.com/partageit/markdown-to-slides
* Tutorial and explanation can be found http://tech.graze.com/2015/07/31/easily-create-slideshow-presentations-from-markdown-with-remark-js/

### Notes on nodejs with brew:
If you initially installed Node.js with Homebrew, run ([link](http://stackoverflow.com/questions/11284634/upgrade-nodejs-to-the-latest-version-on-mac-os)):

Carefull with lat command, better to follow: https://gist.github.com/DanHerbert/9520689
```bash
brew update
brew upgrade node
npm install -g npm
```
Or as a one-liner:

```brew update && brew upgrade node && npm install -g npm```

Other option: https://changelog.com/posts/install-node-js-with-homebrew-on-os-x


* Fixing problems: _Node script executable not working on Mac : env: node\r: No such file or directory_. [Solution](http://stackoverflow.com/questions/30344858/node-script-executable-not-working-on-mac-env-node-r-no-such-file-or-directo):
There is a problem with newlines in your script. Make sure that #! /usr/bin/env node is followed by \n (unix style) instead of \r\n (windows/dos style). To fix that, use the tr command to remove \r's from your file:

```cat your_script.js | tr -d '\r' > fixed_script.js```
