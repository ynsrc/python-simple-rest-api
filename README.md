# Quick Note

I found this quick example [ynsrc/python-simple-rest-api](https://github.com/ynsrc/python-simple-rest-api) of a simple Python API while looking for quick reference to cobble together a quick API for simple a RPI project I am working on (didn't need or want the overhead of FastAPI or equivalent for this simple home project - litterally to set off an animal trap I wanted and API endpoint). I though your little example was spot on for my purposes but there was one thing that I felt could be handled a little bit different and I feel like makes it a little easier extendable and I thought it would be a bit cleaner to remove the ApiRequestHandler definition from inside __main__ and especially with the global api reference.

Basically, all I did was add a method call to the API class that get passed to the HTTPServer instead of the ApiRequestHandler. Internally to the HTTPServer it will "init" the RequestHandlerClass but in this case will just call the API instance. The callable method will then instantiate the ApiRequestHandler passing a reference to the API instance to the ApiRequestHandler without the need for the global in the ApiRequestHandler.

In the ApiRequestHandler all I had to do was initialize the super class passing the same arguments needed for the BaseHTTPRequestHandler while allowing it to pass the api object. Then the API callable returns that ApiRequestHandler object that carries with reference to itself.


# Simple REST API with pure Python

This is an example REST API project.

## Run
```
# python server.py
```

Default port is 5000, you can change it in `server.py`.

## Index
```
$ curl "http://127.0.0.1:5000/"
{
    "name": "Python REST API Example",
    "summary": "This is simple REST API architecture with pure Python",
    "actions": [
        "add",
        "delete",
        "list",
        "search"
    ],
    "version": "1.0.0"
}
```

## List Items
```
$ curl "http://127.0.0.1:5000/list"
{
    "count": 3,
    "items": [
        {
            "id": 1000,
            "name": "cat",
            "description": "cat is meowing"
        },
        {
            "id": 1001,
            "name": "dog",
            "description": "dog is barking"
        },
        {
            "id": 1002,
            "name": "bird",
            "description": "bird is singing"
        }
    ]
}
```

## Search
```
$ curl "http://127.0.0.1:5000/search?q=d"
{
    "count": 2,
    "items": [
        {
            "id": 1001,
            "name": "dog",
            "description": "dog is barking"
        },
        {
            "id": 1002,
            "name": "bird",
            "description": "bird is singing"
        }
    ]
}
```

## Delete Item
```
$ curl "http://127.0.0.1:5000/delete" -H "Content-Type: application/json" -d '{"id": 1001}'
{
    "deleted": 1001
}
```

## Add Item
```
$ curl "http://127.0.0.1:5000/add" -H "Content-Type: application/json" \
> -d '{"name": "fish", "description": "fish is swimming"}'
{
    "id": 1005,
    "name": "fish",
    "description": "fish is swimming"
}
```

## List Again
```
$ curl "http://127.0.0.1:5000/list"
{
    "count": 3,
    "items": [
        {
            "id": 1000,
            "name": "cat",
            "description": "cat is meowing"
        },
        {
            "id": 1002,
            "name": "bird",
            "description": "bird is singing"
        },
        {
            "id": 1003,
            "name": "fish",
            "description": "fish is swimming"
        }
    ]
}
```


# License
The Unlicense. Feel free to use or change it how you need.