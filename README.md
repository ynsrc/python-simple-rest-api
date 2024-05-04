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