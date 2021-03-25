---
title: Third Party Features
---

### Clarifai ImageAPI

Removed Clarifai 


### Text Analytics
#### Yandex Translate API

<img src="https://yastatic.net/www/_/Q/r/sx-Y7-1azG3UMxG55avAdgwbM.svg" width="196" align="right" />

<img src="https://yastatic.net/s3/home/logos/services/1/translate.svg" width="66" align="left" />

###### Offers excellent language detection and synchronized translation for over 95 languages 😎 worldwide

_This service currently is supported only by the [Interact by Comments](#interact-by-comments) feature_.

##### Usage
Go [**sign up**](https://translate.yandex.com/developers/keys) on [_translate.yandex.com_](https://translate.yandex.com) and get a _free_ `API_key`;
_Then configure its usage at your **quickstart** script_,
```python
session.set_use_yandex(enabled=True,
                       API_key='',
                       match_language=True,
                       language_code="en")
```


##### Parameters
`enabled`
: Put `True` to **activate** or `False` to **deactivate** the service usage;

`API_key`
: The _key_ which is **required** to authenticate `HTTP` _requests_ to the **API**;

`match_language`
: **Enable** if you would like to match the language of the text;

`language_code`
: **Set** your desired language's code to **match language** (_if it's enabled_);
>You can get the list of all supported languages and their codes at [_tech.yandex.com_](https://tech.yandex.com/translate/doc/dg/concepts/api-overview-docpage/#api-overview__languages).


##### Rate Limits
In its _free_ plan, the **daily** request _limit_ is `1,000,000` characters and the **monthly** _limit_ is `10,000,000` characters.
>To increase the request limit, you can **switch** to the `fee-based` version of the service (_$`15`/million chars_)..


##### Examples

**1**-) Matching language;
```python
session.set_use_yandex(enabled=True, API_key='', match_language=True, language_code="az")
```
Target text
: "_your technique encourages📸 me_"

_Now that text is gonna be labeled **inappropriate** COS its language is `english` rather than the desired `azerbaijani`_..

**2**-) Enabling the **Yandex** service _but NOT_ matching language;
Since **Yandex** Translate is being used [internally] by the **MeaningCloud** service, you can just provide the API key of **Yandex** and enable it without enabling the `match_language` parameter what will be sufficient for the **MeaningCloud** to work..
```python
session.set_use_yandex(enabled=True, API_key='', match_language=False)
```
>And yes, you can enable **Yandex** service to make it be available for **MeaningCloud** and then also _match language_ if you like, in the same setup just by turning the `match_language` parameter on..


##### Legal Notice
[Powered by Yandex.Translate](http://translate.yandex.com/)

<ins
  class="adsbygoogle"
  data-ad-layout="in-article"
  data-ad-format="fluid"
  data-ad-client="ca-pub-4875789012193531"
  data-ad-slot="9530237054"
></ins>
<script>
  (adsbygoogle = window.adsbygoogle || []).push({});
</script>

#### MeaningCloud Sentiment Analysis API
<img src="https://www.meaningcloud.com/developer/img/LogoMeaningCloud210x85.png" width="210" align="right" />

###### Offers a detailed, multilingual analysis of all kind of unstructured content determining its sentiment ⚖
_This service currently is supported only by the [Interact by Comments](#interact-by-comments) feature_.

Determines if text displays _positive_, _negative_, or _neutral_ sentiment - or is _not possible_ to detect.
Phrases are identified with the _relationship between_ them evaluated which identifies a _global polarity_ value of the text.


##### Usage
**1**-) Go [**sign up**](https://www.meaningcloud.com/developer/login) (_offers **sign in** with_ 😎 _**Github**_) on [_meaningcloud.com_](https://www.meaningcloud.com) and get a _free_ `license_key`;
_Then configure its usage at your **quickstart** script_,
```python
session.set_use_meaningcloud(enabled=True,
                             license_key='',
                             polarity="P",
                             agreement="AGREEMENT",
                             subjectivity="SUBJECTIVE",
                             confidence=94)
```
**2**-) Install its _package_ for **python** by `pip`;
```powershell
pip install MeaningCloud-python
```
**3**-) Turn on **Yandex** _Translate_ service which is a **requirement** for the language _detection_ & _translation_ at request;
_To have it configured, read its [documentation](#yandex-translate-api)_.


##### Parameters
`enabled`
: Put `True` to **activate** or `False` to **deactivate** the service usage;

`license_key`
: The license key is **required** to do _calls_ to the API;

`polarity`
: It indicates the polarity found (_or not found_) in the text and applies to the **global** polarity of the text;
_It's a **graduated** polarity - rates from **very** negative to **very** positive_.

| `score_tag` |                   definition                    |
| ----------- | ----------------------------------------------- |
|    `"P+"`   |       match if text is _**strong** positive_    |
|    `"P"`    |       match if text is _positive_ or above      |
|    `"NEU"`  |       match if text is _neutral_ or above       |
|    `"N"`    |       match if text is _negative_ or above      |
|    `"N+"`   | match if text is _**strong** negative_ or above |
|    `None`   |     do not match per _polarity_ found, at all   |

  > By "_or above_" it means- _e.g._, if you set `polarity` to `"P"`, and text is `"P+"` then it'll also be appropriate (_as it always leans towards positivity_) ..

`agreement`
: Identifies **opposing** opinions - _contradictory_, _ambiguous_;
_It marks the agreement **between** the sentiments detected in the text, the sentence or the segment it refers to_.

|    `agreement`   |                            definition                                     |
| ---------------- | ------------------------------------------------------------------------- |
|   `"AGREEMENT"`  |       match if the different elements have **the same** polarity          |
| `"DISAGREEMENT"` | match if there is _disagreement_ between the different elements' polarity |
|      `None`      |              do not match per _agreement_ found, at all                   |


`subjectivity`
: Identification of _opinions_ and _facts_ - **distinguishes** between _objective_ and _subjective_;
_It marks the subjectivity of the text_.

| `subjectivity` |                          definition                           |
| -------------- | ------------------------------------------------------------- |
| `"SUBJECTIVE"` |           match if text that has _subjective_ marks           |
| `"OBJECTIVE"`  | match if text that does not have **any** _subjectivity_ marks |
|     `None`     |         do not match per _subjectivity_ found, at all         |

`confidence`
: It represents the _confidence_ associated with the sentiment analysis **performed on the** text and takes an integer number in the _range of_ `(0, 100]`;
>If you **don't want to** match per _confidence_ found, at all, use the value of `None`.


##### Rate Limits
It gives you `20 000` single API calls per each month (_starting from the date you have **signed up**_).
It has _no daily limit_ but if you hit the limit set for number of requests can be carried out concurrently (_per second_) it'll return with error code of `104` rather than the result 😉


##### Language Support
**MeaningCloud** currently supports a generic sentiment model (_called general_) in these languages: _english_, _spanish_, _french_, _italian_, _catalan_, and _portuguese_.
>You can define your own sentiment models using the user sentiment models console and work with them in the same way as with the sentiment models it provides.

But **no need to worry** IF your _language_ or _target audience's language_ is NONE of those **officially** supported.
Cos, to **increase the coverage** and support **all other** languages, as well, **Yandex** _Translate_ service comes to rescue!
It detects the text's langugage before passing it to **MeaningCloud**, and, if its language is not supported by **MeaningCloud**, it translates it into english and only then passes it to **MeaningCloud** _Sentiment Analysis_..


##### Examples
**a** -) Match **ONLY** per `polarity` and `agreement`
```python
session.set_use_meaningcloud(enabled=True, license_key='', polarity="P", agreement="AGREEMENT")
```
Target text
: "_I appreciate your innovative thinking that results, brilliant images_"

_Sentiment Analysis_ results for the text:

| `score_tag` |  `agreement`  | `subjectivity` | `confidence` |
| ----------- | ------------- | -------------- | ------------ |
|   `"P+"`    | `"AGREEMENT"` | `"SUBJECTIVE"` |     `100`    |

_Now that text is gonna be labeled **appropriate** COS its polarity is `"P+"` which is more positive than `"P"` and `agreement` values also do match_..

**b** -) Match **FULLY**
```python
session.set_use_meaningcloud(enabled=True, license_key='', polarity="P+", agreement="AGREEMENT", subjectivity="SUBJECTIVE", confidence=98)
```
Target text
: "_truly fantastic but it looks sad!_"

_Sentiment Analysis_ results for the text:

| `score_tag` |    `agreement`   | `subjectivity` | `confidence` |
| ----------- | ---------------- | -------------- | ------------ |
|    `"P"`    | `"DISAGREEMENT"` | `"SUBJECTIVE"` |     `92`    |

_Now that text is gonna be labeled **inappropriate** COS its polarity is `"P"` which is less positive than `"P+"` and also, `agreement` values also **do NOT** match, and **lastly**, `confidence` is **below** user-defined `98`_..


##### Legal Notice
This project uses MeaningCloud™ (http://www.meaningcloud.com) for Text Analytics.

<ins
  class="adsbygoogle"
  data-ad-layout="in-article"
  data-ad-format="fluid"
  data-ad-client="ca-pub-4875789012193531"
  data-ad-slot="9530237054"
></ins>
<script>
  (adsbygoogle = window.adsbygoogle || []).push({});
</script>

---

### Telegram Integration

This feature allows to connect your InstaPy session with a Telegram bot and send commands
to the InstaPy session

#### Prerequisites
You will need to create a token, for this go into your Telegram App and talk with @fatherbot.
You will also need to set your username as it is checked to ensure that you are authorized to
access the InstaPy session, to do so go to Settings -> Profile -> Username.

#### Supported actions
There are 3 supported actions:
  - /start : will start the interaction between the bot and instapy. Please note: that the telegram bot
  cannot send you messages until you first send it a /start message. The bot will store the chat_id in the logs folder
  file telegram_chat_id.txt to be reused in further sessions (so you have to actually do /start just one time)
  - /report : will gather and show the current session statistics
  - /stop: will set the aborting flag to True

#### Examples
```python
from instapy.plugins import InstaPyTelegramBot

        session = InstaPy(username=insta_username,
                          password=insta_password,
                          bypass_with_mobile=True)

        telegram = InstaPyTelegramBot(token='insert_real_token_here', telegram_username='my_username', instapy_session=session)

        # if you want to receive the information when the session ends
        # just add the following before your session.end()
        telegram.end()
        session.end()
````

Additional parameters:
   - debug=True if you want low level telegram debug information
   - proxy if you need one, here is the structure that needs to be passed

```python
    example_proxy = {
         'proxy_url': 'http://PROXY_HOST:PROXY_PORT/',
         # Optional, if you need authentication:
         'username': 'PROXY_USER',
         'password': 'PROXY_PASS',
     }
     telegram = InstaPytelegramBot(... , proxy=example_proxy)
```

#### Additional functionality
you can use
```python
telegram.send_message(text="this is a message")
```

So you are able to send additional message inside your script if needed. Remember that the telegram bot  
is not able to send messages as long as you haven't done at least one `/start`.
