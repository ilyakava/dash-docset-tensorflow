# dash-docset-tensorflow

![screenshot](/screenshot.png)

View TensorFlow docs in the [dash](https://kapeli.com/dash)/[zeal](https://github.com/zealdocs/zeal) offline docset browser.

## Dash/Zeal Feeds

To use, you can add the following feeds in Dash/Zeal:
- v1.15: `https://raw.githubusercontent.com/ilyakava/dash-docset-tensorflow/master/TensorFlow-v1.15.xml`

Or download archived docsets as releases [here](https://github.com/ilyakava/dash-docset-tensorflow/releases).

## Steps to generate the docset
+ Install [dashing](https://github.com/technosophos/dashing): `go get -u github.com/technosophos/dashing`
+ `pip install --user python-magic beautifulsoup4 lxml`
+ `cd THIS_REPO`
+ `wget -nc -np --domains=www.tensorflow.org -e robots=off --adjust-extension -r 'https://www.tensorflow.org/api_docs/'`
+ `cp dashing.json icon*.png main.css www.tensorflow.org`
+ `./preprocess.sh www.tensorflow.org`
+ `cd www.tensorflow.org/`
+ `dashing build` will give you a `TensorFlow.docset` folder.

Right now this `dashing.json` only roughly parses function names (which is enough for most use cases).
Feel free to add more features and contribute!

## Installing a local docset into Zeal
+ Make an archive: `tar --exclude='.DS_Store' -cvzf <docset name>.tgz <docset name>.docset`
+ Make an xml file whose name will be the docset display name in Zeal. Its contents should be:
```
<entry>
    <version>1.15</version>
    <url>file:///path/to/archive/TensorFlow-vX.X.docset.tgz</url>
</entry>
```
+ In Zeal go to Tools > Docsets > Add feed and for url type 'file:///path/to/docset.xml'
