# ArtML


**Artml is a xml based standart for containing articles**


## Article element
- article is a root element
- attrubites in an article element discribe article. full list of them:
    - title **required**
    - publish, date of publish in ISO 8601
    - edit, date of last edit in ISO 8601
    - except. should not inclide double quote symbol - < " >
    - front, url to an image that are stands as header or as cover. check [this](#url-rules) for url rules
    - language, language in ISO 639-2 format (always 3 characters). eng for english  **required** 
- the only allowed xml encoding utf-8 others will be considered as errors
- only allowed xml version is 1.0 others will be considered as errors

        <?xml version="1.0" encoding="UTF-8"?>
        <article>
            <p>
                hello world
            </p>
        </article>


## Elements that can be used in artml

### p
tag can contain all set of characters (except '<' and '>') and tag tm (which stands for text modify). p tag can't contain another p tag

### tm
can have followed attributes. content of them does not matter if other is not specified but it have to be something for example empty string (it's xml standart but worth mentioning)

- src - makes a link, check [this](#url-rules) for url rules
- bold - makes bold text, if it's important (strong in html) should have "n" inside
- italic - makes italic text, if it's emphasised (em in html) should have "n" inside
- q - makes quote, contains source of quote. if have to be same as src attribute it should have "a" inside, if doesn't have any source it should have value null q="null" (cite attribute for html)

      <p> hello friend, <tm bold="anything - jfkasdjasfasdfasdfasdf, this will be ignored"> nice to meet you again </tm></p>
      <tm bold="n"> important</tm>
      
      //<tm bold>text</tm> is INVALID


### q(quote)
tag contain same set of characters and tags as p tag does. quote tag can have p tag inside, but can't have tm tags with "q" attribute

    <p>They said </p>
    <q>it cannot be done</q>


### ul, ol
tags very similar to html version. it can only contain li tags inside.

### li
tag is an item for lists(ul, ol tags). can contain text and tm tags. li tag can have same attributes as tm tag do except 'q' attribute.

    <ul>
        <li bold="">hello</li>
    </ul>

### image
tag contain url to an image, check [this](#url-rules) for url rules.
images can be in these formats: png, jpg(jpeg), webp, gif

can have followed attributes:

- w, for defining width of an image in pixels **required**
- h, for defining hegith of an image in pixels **required**


        <image w="1300" h="1300">s:api.sveagruva.site/static/thor/1.png</image>
    

### video
tag contain url to a video, check [this](#url-rules) for url rules
can have followed attributes:

- w, for defining width of an video in pixels **required**
- h, for defining hegith of an video in pixels **required**

        <video w="1300" h="1300">s:example.com/video.mp4</video>


### slider
tag can contain only image tags

    <slider> 
        <image w="1300" h="1300">s:api.sveagruva.site/static/thor/1.png</image>
        <image w="1300" h="1300">s:api.sveagruva.site/static/thor/1.png</image>
    </slider>


### twitter
tag contains 18 digits otherwise not valid

    <tiwtter>123456789012345678</twitter>

### yb(youtube)
tag contains 11 characters otherwise not valid

    <yb>12345678901</yb>





## Url rules
url starts with s for https and with p for http  and followed by ':' symbol. the rest part is the rest part of a link. for example:

        s:api.sveagruva.site/static/thor/1.png
        
mean

        https://api.sveagruva.site/static/thor/1.png
        
for describing resources that have to be transferred another way can be used l protocol or any other protocol that you can make yourself that are started with l
        
        l:/base64/image/png/1
        l_my_protocol:/base64/image/png/1
