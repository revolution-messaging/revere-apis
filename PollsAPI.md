# Polls API

HOST: http://polls.apiblueprint.org/

Polls is a simple API allowing consumers to view polls and vote in them.

## Questions Collection

### List All Questions
```
GET /questions
```
**Response**
```json
Status: 200
[
    {
        "question": "Favourite programming language?",
        "published_at": "2015-08-05T08:40:51.620Z",
        "choices": [
            {
                "choice": "Swift",
                "votes": 2048
            }, {
                "choice": "Python",
                "votes": 1024
            }, {
                "choice": "Objective-C",
                "votes": 512
            }, {
                "choice": "Ruby",
                "votes": 256
            }
        ]
    }
]
```
### Create a New Question
```
POST /questions
```
You may create your own question using this action. It takes a JSON
object containing a question and a collection of answers in the
form of choices.

**Request**
```json
{
    "question": "Favourite programming language?",
    "choices": [
        "Swift",
        "Python",
        "Objective-C",
        "Ruby"
    ]
}
```

**Response**
```json
Status: 201
{
    "question": "Favourite programming language?",
    "published_at": "2015-08-05T08:40:51.620Z",
    "choices": [
        {
            "choice": "Swift",
            "votes": 0
        }, {
            "choice": "Python",
            "votes": 0
        }, {
            "choice": "Objective-C",
            "votes": 0
        }, {
            "choice": "Ruby",
            "votes": 0
        }
    ]
}
```
