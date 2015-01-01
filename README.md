[![Build Status](https://travis-ci.org/peachjean/dnsfiles.svg)](https://travis-ci.org/peachjean/dnsfiles)

This is a simple python script that will allow us to update gandi dns based on 
some zone files stored on disk.

My goal is to create a free version of the "github in dns" tools. We should be 
able to use travis to update our DNS provider with the information that we've 
stored in github. I'm starting with gandi, since that's what I use.

My intention is to write a python script that gets all of the info that it 
needs from the local directory structure. Then we can deploy that script to
pypi. Then, we simply setup a travis build with this script in 
``requirements.txt``, a command to run the script, and our DNS API credentials
encrypted in the ``.travis.yml`` file.

So your ``.travis.yml`` file would look something like this: (pending actually
writing the script)

```yaml
language: python
python:
  - "3.4"
install:
  - "pip install github-dns"
script: "github-dns"
env:
  - secure: <encrypted gandi creds>
```

Then you setup a travis build and you're good to go.

