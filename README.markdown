# TwitterSearch
[![Build](https://api.travis-ci.org/ckoepp/TwitterSearch.png?branch=master)](https://travis-ci.org/ckoepp/TwitterSearch) [![Downloads](https://pypip.in/d/TwitterSearch/badge.png)](https://crate.io/packages/TwitterSearch/) [![PyPI version](https://pypip.in/v/TwitterSearch/badge.png)](https://crate.io/packages/TwitterSearch/)


This library allows you easily create a search through the Twitter Search API without having to know too much about the API details. Based on such a search you can even iterate throughout all tweets reachable via the Twitter Search API. There is an automatic reload of the next pages while using the iteration.

## Reasons to use TwitterSearch
Well, because it can be quite annoying to always parse the search url together and a minor spelling mistake is sometimes hard to find. Not to mention the pain of getting the next page of the results. Why not centralize this process and concentrate on the more important parts of the project?

More than that, TwitterSearch is:
 * pretty small (around 300 lines of code currently)
 * pretty easy to use, even for beginners
 * pretty good at giving you ALL available information (including meta information)
 * pretty iterable without any need to manually reload more results from the API
 * pretty wrong values of API arguments are to raise an exception. This is done before the API gets queried and therefore helps to avoid to reach Twitters' limitations by obviously wrong API calls
 * pretty pretty to look at :)

## Example
The library is still in an early stage. However, if you would like to use it we prepared a small example about how to play around. 

Everybody knows how much work it is to study at a university. So why not take a small shortcut? So in this example we assume we would like to find out how to copy a doctorate thesis in Germany. Let's have a look what the Twitter users have to say about [Mr Guttenberg](http://www.bbc.co.uk/news/world-europe-12608083).

```python
from TwitterSearch import *
try:
    tso = TwitterSearchOrder() # create a TwitterSearchOrder object
    tso.setKeywords(['Guttenberg', 'Doktorarbeit']) # let's define all words we would like to have a look for
    tso.setLanguage('de') # we want to see German tweets only
    tso.setCount(7) # please dear Mr Twitter, only give us 7 results per page
    tso.setIncludeEntities(False) # and don't give us all those entity information

    # it's about time to create a TwitterSearch object with our secret tokens
    ts = TwitterSearch(
        consumer_key = 'aaabbb',
        consumer_secret = 'cccddd',
        access_token = '111222',
        access_token_secret = '333444'
     )

    for tweet in ts.searchTweetsIterable(tso): # this is where the fun actually starts :)
        print( '@%s tweeted: %s' % ( tweet['user']['screen_name'], tweet['text'] ) )

except TwitterSearchException as e: # take care of all those ugly errors if there are some
    print(e)
```
The result will be a text looking similar to this one. But as you see unfortunately there is no idea hidden in the tweets how to get your doctorate thesis without any work. Damn it!
```
@enricozero tweeted: RT @viehdeo: Archiv: Comedy-Video: Oliver Welke parodiert “Mogelbaron” Dr. Guttenbergs Doktorarbeit (Schummel-cum-laude Pla... http://t. ...
@schlagworte tweeted: "Erst letztens habe ich in meiner Doktorarbeit Guttenberg zitiert." Blockflöte des Todes: http://t.co/pCzIn429
@nkoni7 tweeted: Familien sind auch betroffen wenn schlechte Politik gemacht wird. Nicht nur wenn Guttenberg seine Doktorarbeit fälscht ! #absolutemehrheit
```

##Wanna see more details?
If you'd like to get more information about how TwitterSearch works interally and how to use it with all it's possibilities have a look at the [Wiki](https://github.com/ckoepp/TwitterSearch/wiki).

##License (MIT)
Copyright (C) 2013 Christian Koepp

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
