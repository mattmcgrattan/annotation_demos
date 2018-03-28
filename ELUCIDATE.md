# Annotation Dev Samples

## Basics

### Create container

```commandline
POST /annotation/w3c/ HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
Slug: my-container
Host: annotation-dev.digtest.co.uk
Connection: close
Content-Length: 214

{
  "@context": [
    "http://www.w3.org/ns/anno.jsonld",
    "http://www.w3.org/ns/ldp.jsonld"
  ],
  "type": [
    "BasicContainer",
    "AnnotationCollection"
  ],
  "label": "A Container for Web Annotations"
}

```
### Create annotation

```commandline
POST /annotation/w3c/my-container/ HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
Host: annotation-dev.digtest.co.uk
Connection: close
Content-Length: 203

{
  "@context": "http://www.w3.org/ns/anno.jsonld",
  "type": "Annotation",
  "body": {
    "type": "TextualBody",
    "value": "I like this page!"
  },
  "target": "http://www.example.com/index.html"
}

```
### Get annotation container

```commandline
GET /annotation/w3c/my-container/ HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
Host: annotation-dev.digtest.co.uk
Connection: close
```

### Get annotation 

```commandline
GET /annotation/w3c/my-container/0311cac0-f093-43c6-bdc1-4ec3c0c61f92 HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
Host: annotation-dev.digtest.co.uk
Connection: close
```

### Update annotation

```commandline
PUT /annotation/w3c/my-container/0311cac0-f093-43c6-bdc1-4ec3c0c61f92 HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
If-Match: a3c9b1580154b1e33fa088c72bb8be26
Host: annotation-dev.digtest.co.uk
Connection: close
Content-Length: 246

{
  "@context": "http://www.w3.org/ns/anno.jsonld",
  "type": "Annotation",
  "created": "2015-01-31T12:03:45Z",
  "body": {
    "type": "TextualBody",
    "value": "I don't like this page!"
  },
  "target": "http://www.example.com/index.html"
}
```

## Searches

### Search by target (prefix)

#### Request

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/target?fields=source&value=https://presley.glam-dev.org

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
```

### Search by target (strict, whole canvas)

#### Request

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/target?fields=source&value=https://presley.glam-dev.org/iiif/test/_roll_M-1011_174_cvs-30-52/canvas/c44&strict=true

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
```
### Search by target (Media Fragment)

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/target?fields=source&value=https:%2F%2Fpresley.glam-dev.org%2Fiiif%2Ftest%2F_roll_M-1011_174_cvs-30-52%2Fcanvas%2Fc44&xywh=1060,1800,400,75

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search by target and creator


```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/target?fields=source&value=https:%2F%2Fpresley.glam-dev.org%2Fiiif%2Ftest%2F_roll_M-1011_174_cvs-30-52%2Fcanvas%2Fc44&creator=https:%2F%2Fusers.glam-dev.org%2F1

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search by target (prefix) and creator

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/target?fields=source&value=https:%2F%2Fpresley.glam-dev.org%2Fiiif%2Ftest%2F_roll_M-1011_174_cvs-30-52&creator=https:%2F%2Fusers.glam-dev.org%2F1

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search by creator id

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/creator?fields=source&value=https:%2F%2Fusers.glam-dev.org%2F1&strict=true&levels=annotation&type=id

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search by body source

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/body?fields=source&value=https:%2F%2Fomeka.dlcs-ida.org%2Ftopics%2Fgpe%2Fzuni&strict=true

Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search by body source (prefix: topic type example)

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/body?fields=source&value=https:%2F%2Fomeka.dlcs-ida.org%2Ftopics%2Fgpe%2F&strict=False
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

### Search temporal (created since)

```
GET https://annotation-dev.digtest.co.uk/annotation/w3c/services/search/temporal?since=2018-02-18T19:48:50.000Z&levels=annotation&types=created
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

```

## Statistics

### Body

```commandline
GET /annotation/w3c/services/stats/body?field=source HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Host: annotation-dev.digtest.co.uk
Connection: close
```

### Target

```commandline
GET /annotation/w3c/services/stats/target?field=source HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Host: annotation-dev.digtest.co.uk
Connection: close
```

## Bulk Update

```commandline
POST /annotation/w3c/services/batch/update HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Content-Type: application/ld+json;
Host: annotation-dev.digtest.co.uk
Connection: close
User-Agent: Paw/3.1.5 (Macintosh; OS X/10.13.3) GCDHTTPRequest
Content-Length: 391

{
  "@context": "http://www.w3.org/ns/anno.jsonld",
  "body": {
    "id": "https://omeka.dlcs-ida.org/topics/virtual:org/thora",
    "oa:isReplacedBy": "https://omeka.dlcs-ida.org/topics/virtual:org/thora+hird",
    "source": {
      "id": "https://omeka.dlcs-ida.org/topics/virtual:org/thora",
      "oa:isReplacedBy": "https://omeka.dlcs-ida.org/topics/virtual:org/thora+hird"
    }
  }
}
```

## Annotation History

```commandline
GET /annotation/w3c/f94bd5abf5d3b275f664fcb747c6d09e/c781fa96-e185-4ae6-8e81-30ed8d1568f5 HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Host: annotation-dev.digtest.co.uk
Connection: close
```

Response

```commandline
HTTP/1.1 200 
Server: nginx
Date: Sun, 18 Feb 2018 21:44:42 GMT
Content-Type: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld";charset=UTF-8
Transfer-Encoding: chunked
Connection: close
ETag: W/"1e9c4cdadcd6f564981f1980d176b38b"
Link: <http://www.w3.org/ns/ldp#Resource>; rel="type"
Link: <https://annotation-dev.digtest.co.uk/annotation/w3c/services/history/f94bd5abf5d3b275f664fcb747c6d09e/c781fa96-e185-4ae6-8e81-30ed8d1568f5/1>; rel="prev memento"; datetime="Sun, 18 Feb 2018 19:49:42 UTC"
Allow: PUT,GET,OPTIONS,HEAD,DELETE
Vary: Accept
Memento-Datetime: Sun, 18 Feb 2018 21:40:02 UTC
```

Get the earlier version:

```commandline
GET /annotation/w3c/services/history/f94bd5abf5d3b275f664fcb747c6d09e/c781fa96-e185-4ae6-8e81-30ed8d1568f5/1 HTTP/1.1
Accept: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"
Host: annotation-dev.digtest.co.uk
Connection: close
```


