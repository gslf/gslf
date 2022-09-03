# [NLP] nltk Downloader



The **nltk** library of python3 comes with a useful downloader with a graphical interface for managing packages.

Unfortunately, if you try to start the downloader GUI from Mac or if you launch the download function via CLI,  you will see an error like this:

```
>> nltk.download('averaged_perceptron_tagger')
[nltk_data] Error loading averaged_perceptron_tagger: <urlopen error [SSL:
[nltk_data]     CERTIFICATE_VERIFY_FAILED] certificate verify failed
[nltk_data]     (_ssl.c:590)>
False
```

To solve this, you need to create an SSL context that is considered valid. This snippet does just that: it creates the context and starts the downloader GUI, from which you can download the necessary packages and monitor the packages.

```
import nltk
import ssl

try:
    _create_unverified_https_context = ssl._create_unverified_context
except AttributeError:
    pass
else:
    ssl._create_default_https_context = _create_unverified_https_context

nltk.download()
```

Thanks to [stackoverflow](https://stackoverflow.com/questions/38916452/nltk-download-ssl-certificate-verify-failed) to solve my problems!


