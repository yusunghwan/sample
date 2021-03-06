Lifemedia API m8l6 ll 
============================

lj5,l,m-
-----------

lk k*lk ml
$m
8 k*k 9l  POSIX mj2=ll lm	ml l<k)0 k$lj3< j0l  mk!j78k(l mlk! m(.

* curl (ml)

* xmllint (l m, libxml2)
* xml2json (l m, `npm`l<k! l$l9)
* jq (l m, jq)



l4j80m
---------

```sh
API_PATH="http://lifemedia.video.kiwiple.net/api"
API_USERNAME=l,l)m  j3l 

API_TOKEN=$(curl -s -X POST "$API_PATH/login2" -d "username=$API_USERNAME" | jq -r .token)

alias lmcurl='curl -s -H "Authorization: $API_TOKEN"'
```

m m0 k0j8	
----------------

(l4j80m ll ll k/8k&, k0j8	k0l)

* Endpoint: `POST` `/login2`

* Form parameters:
    - `username`: l,l)m  j3l 

* Response data:
    - `token`: l8l& m m0
    - `duration`: l8l& m m0 k'k#j9l'  k(l  lj0 (l4)

### m8l6 ll 

```sh
$ curl -s -X POST "$API_PATH/login2" -d "username=$API_USERNAME" | jq .
```

```json
{
  "duration": "86400",
  "token": "eyJhbGciOiJIU234sdf89h25lkjhHJKGDF78gsLFHJGhjsd982734234MjExMjgyfQ.eyJpZCI6MX0.RPantFZ0TNCf9879JKHKFGDceAa7_j1Kj8cF1IRnxR8"
}
```


l1k l!0m
-----------

* Endpoint: `GET` `/channel2`

* Query parameters:
    - `limit`: ml4l' k9 mlm  m-k*) l. j80k38j0 20
    - `cursor`: k$l ml4l' k%< l!0mmj80 lm j0. lk5l `//Paging/Next/text()` j0 l,l)
    - `sort`: l k , ll. asc: ll1l<l j3<j10-l5l  l / desc: ll1l<l l5l -j3<j10 l
    - `start_date`: ll1l<lj0  `start_date` l4ll8 m-k*)k' l!0m. `YYYY-MM-DD` ml.
    - `end_date`: ll1l<lj0  `end_date` l4ml8 m-k*)k' l!0m. `YYYY-MM-DD` ml.
    - `hashtag_ids`: l' l m m4lmj78 IDk$l l,l)m m-k*)k' l!0m. `1,2,3,4,5` ml


* Response data: (XML)
    - `//Paging`: ml4l' l k34
        * `Next`: k$l ml4l' l l$ml
        * `Paging` kk
 `Next`j0  lk
 j2=l0 k'l' k'	 ml4l' k%< k;m(.
    - `//ServiceInformation[]`
        * `recentPlay`: l4l4k34j80 l k34
            - `offset`: l,l ll9. m4k<l4l8m
8ll l l!m j0l j78k k! k0m
            - `modificationTime`: k'l' k'	 l,l lj0. RFC 3339 ml.
        * `hashtagList`: m4lmj78 k*)k!
            - `Hashtag`: m4lmj78.
                - `id` ll1: m4lmj78 ID
                - j0: m4lmj78 k*
        * `favorite`: l&j2(l0>j80 l k34
            - `creationTime`: l&j2(l0>j80k! l6j0 m lj0. RFC 3339 ml

### m8l6 ll 

```sh
$ lmcurl "$API_PATH/channel2"  | xmllint --pretty 1 -
$ lmcurl "$API_PATH/channel2?cursor=kpLXAcCX3NttIgUAVoA&limit=10&sort=asc&start_date=2015-01-01&end_date=2015-12-31&hashtag_ids=1,2,3,4,5,6,7"  | xmllint --pretty 1 -
```

```
<?xml version="1.0" encoding="utf8"?>
<epg xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" creationTime="2015-12-04T06:58:27Z" epgId="" userId="1" version="2">
  <Paging>
    <Next>kpLXAcCX3NttIgUAVoA</Next>
  </Paging>
  <ServiceInformation>
    <subtitle_url/>
    <content_description/>
    <user_id>1</user_id>
    <content_title>today</content_title>
    <channel_name>test</channel_name>
    <service_mode>private</service_mode>
    <creation_time>2015-10-21 06:17:46</creation_time>
    <content_url>http://video.kiwiple.net/movie/baaac5352ca94949ab48d2addf1e34ef</content_url>
    <channel_number>7</channel_number>
    <content_thumbnail/>
    <content_type>video</content_type>
    <content_number>104</content_number>
    <duration>0</duration>
    <service_language>korean</service_language>
    <id>104</id>
    <favorite>
      <creationTime>2015-12-04T03:34:50Z</creationTime>
    </favorite>
    <recentPlay>
      <offset>aabc</offset>
      <modificationTime>2015-12-04T03:34:41Z</modificationTime>
    </recentPlay>
    <hashtagList>
      <Hashtag id="1">mj88k</Hashtag>
      <Hashtag id="5">mj88kl </Hashtag>
      <Hashtag id="7">k<k'k0</Hashtag>
      <Hashtag id="8">345345</Hashtag>
    </hashtagList>
  </ServiceInformation>
...
```


l&j2(l0>j80 k1k!
--------------------------

* Endpoint: `PUT` `/channel/{id}/favorite`

### m8l6 ll 

```sh
$ lmcurl -X PUT "$API_PATH/channel/104/favorite"
```

```
{}
```

l&j2(l0>j80 l-l 
--------------------------

* Endpoint: `DELETE` `/channel/{id}/favorite`



l4l4k34j80 l k34 j80k!
--------------------------

* Endpoint: `PUT` `/channel/{id}/last-offset`

* Form parameters:
    - `offset`: l5l" l,l ll9. lll k,8ll4

### m8l6 ll 

```sh
$ lmcurl -X PUT "$API_PATH/channel/104/last-offset" -d offset=aabc
```

```
{}
```

l4l4k34j80 l k34  l-l 
--------------------------

* Endpoint: `DELETE` `/channel/{id}/last-offset`



m4lmj78 k1k!
--------------------------

* Endpoint: `POST` `/hashtag`

* Form parameters:
    - `name`: m4lmj78k*

* Response data:
    - `id`: ll1k m4lmj78 ID

### m8l6 ll 

```sh
$ lmcurl -X POST "$API_PATH/hashtag" -d name=m4lmj78 | jq .
```

```
{
  "id": 9
}
```

m4lmj78 l!0m
--------------------------

* Endpoint: `GET` `/hashtag`

* Query parameters:
    - `q`: j2 l	m  m4lmj78k*. k/8l' l l l,l)lj0  l,l)m l l24 m4lmj78 k0m.
       - l,k, j0 l' l m  j2=l0 j0m	k,8lk! j5,k6ml, lk %mk$. ex)m4lmj78\nmj88k


### m8l6 ll  - m4lmj78 j2 l	

```sh
$ lmcurl -v "$API_PATH/hashtag" --get --data-urlencode $'q=m4lmj78\nmj88k'  | jq .
```

```json
{
  "list": [
    {
      "id": 1,
      "name": "mj88k"
    },
    {
      "id": 9,
      "name": "m4lmj78"
    }
  ]
}
```


### m8l6 ll  - (l,l)lj0 ) l,l)m l l24 m4lmj78 k*)k!

```sh
$ lmcurl "$API_PATH/hashtag"
```

```json
{
  "list": [
    {
      "id": 1,
      "name": "mj88k"
    },
    {
      "id": 5,
      "name": "mj88kl "
    },
    {
      "id": 7,
      "name": "k<k'k0"
    },
    {
      "id": 8,
      "name": "345345"
    }
  ]
}
```

klll m4lmj78 l' l 
--------------------------

* Endpoint: `PUT` `/channel/{id}/hashtag`

* Form parameters:
    - `hashtag`: m4lmj78 ID k*)k!. ,k! j5,k6ml, l' l 

### m8l6 ll 

```sh
$ lmcurl -X PUT "$API_PATH/channel/104/hashtag" -d "hashtags=1,5,6,7,8"
```

```
{}
```


### l$k% ll  - l!4l,ml'  l
k
 m4lmj78 l' l l

```sh
$ lmcurl -X PUT "$API_PATH/channel/104/hashtag" -d "hashtags=1,2,3,4,5,6,7,8" | jq .
```

```
{
  "message": "Hashtag not found: 2,3,4",
  "status_code": 500
}
```
