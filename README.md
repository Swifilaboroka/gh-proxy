gh-proxy
Introduction
An acceleration project for github release, archive, and project files, supports cloning, has a Cloudflare Workers serverless version and a Python version

Demo
https://gh.api.99988866.xyz/

The demo site is a public service. If you need large-scale use, please deploy it yourself. The demo site is a bit overwhelmed.

imagea272c95887343279.png

Donations are of course also welcome to support the author

Differences between Python version and CF worker version
The Python version supports file size limits. If the file size exceeds the limit, the original address will be returned. Issue #8

Python version supports specific user/repo ban/whitelist and passby issue #41

use
https://gh.api.99988866.xyz/Just add it before the copied URL

You can also access it directly by typing in

Please deploy it yourself for large-scale use. The above domain names are only for demonstration purposes.

Access to private repositories can be done through

git clone https://user:TOKEN@ghproxy.com/https://github.com/xxxx/xxxx #71

The following are all legal inputs (examples only, the file does not exist):

Branch source code: https://github.com/hunshcn/project/archive/master.zip

Release source code: https://github.com/hunshcn/project/archive/v0.1.0.tar.gz

Release file: https://github.com/hunshcn/project/releases/download/v0.1.0/example.zip

Branch file: https://github.com/hunshcn/project/blob/master/filename

commit file: https://github.com/hunshcn/project/blob/1111111111111111111111111111/filename

gist：https://gist.githubusercontent.com/cielpy/351557e6e465c12986419ac5a4dd2568/raw/cmd.py

cf worker version deployment
Home page: https://workers.cloudflare.com

Register, log in Start building, get a subdomain, Create a Worker.

Copy index.js to the code box on the left Save and deploy. If normal, the homepage should be displayed on the right.

ASSET_URLIt is the URL of the static resource (actually the single page of the input box displayed now)

PREFIXIt is a prefix. By default (root path is "/"). If the custom route is example.com/gh/*, please change PREFIX to '/gh/'. Note that any missing dash will be wrong!

Python version deployment
Docker deployment
docker run -d --name="gh-proxy-py" \
  -p 0.0.0.0:80:80 \
  --restart=always \
  hunsh/gh-proxy-py:latest
The first port 80 is the port you want to expose.

Direct deployment
Install dependencies (please use python3)

pip install flask requests

app/main.pyThe first few configurations modified as needed

Note: You may need to add two lines return Responsebefore

if 'Transfer-Encoding' in headers:
    headers.pop('Transfer-Encoding')
Notice
If the Python version of the machine cannot access github.io normally, an error will be reported. Please modify the static file URL yourself.

The Python version uses the server by default (updated on March 27, 2021)

Cloudflare Workers billing
Go to overviewthe page to see the usage. The free version has 100,000 free requests per day and a limit of 1,000 requests per minute.

If that is not enough, you can upgrade to the $5 premium version, which provides 10 million requests per month (exceeding $0.5/million requests).

Changelog
2020.04.10 Added raw.githubusercontent.comsupport for files
2020.04.09 Added Python version (using Flask)
2020.03.23 Added support for clone
2020.03.22 Initial version
Link
My Blog

reference
jsproxy

Donate
wx.png ali.png
