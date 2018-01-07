## Summary

This repo is a practice of building RESTful API by Python Flask Framework.
All the step is followed by [youtube channel](https://www.youtube.com/watch?v=CjYKrbq8BCw&list=PLXmMXHVSvS-AFMUmbBeIfL3PqTvgw8ygb) created by Pretty Printed.

## RESTful API

RESTful API is just a type of coding format or style that everyone develops, then front-end and back-end engineer can easily cooperate with these rules.

RESTful API compose 4 main methods for response to each HTTP request :

* GET - Retuen all the info which the user should get
* POST - Get the info from the user and optionally return the data
* PUT - Modify certain info
* DELETE - Delete certain info

Normally, user use RESTful API to interact with database, including query or put the data by Requesting the URL. Each URL have its own things to do (i.e., View Function).

## Usage

Download the repo, and under the directory run:

    python restful.py

Everything should work fine.

## Data

For now, we don't truly interact with database. We just put a dictionary to store some info in it, and use Postman to interact with these API.

languages = [{'name': 'JavaScript'}, {'name': 'Python'}, {'name': 'Ruby'}]

## GET Request

** To test if the API server is running **

    @app.route('/', methods=['GET'])
    def test():
        return jsonify({'message': 'It works!'})

Open http://127.0.0.1:8080/ will automatically throw a HTTP request which will show

    {
         "message": "It works!"
    }

** Show all the language **

    @app.route('/lang', methods=['GET'])
    def returnAll():
        return jsonify({'languages':languages})

Open http://127.0.0.1:8080/lang will show

    {
      "languages": [
        {
          "name": "JavaScript"
        }, 
        {
          "name": "Python"
        }, 
        {
          "name": "Ruby"
        }
      ]
    }

** Show one language **

    @app.route('/lang/<string:name>')
    def returnOne(name):
        langs = [language for language in languages if language['name'] == name]
        return jsonify({'language': langs[0]})

<string:name\> means this will accept a variable named *name* and the type is *string*

Open http://127.0.0.1:8080/lang/JavaScript will show

    {
      "language": {
        "name": "JavaScript"
      }
    }

## POST Request

*TO test the requests exclude GET, we have to use [Postman](https://www.getpostman.com)*

** Add a new language **

    @app.route('/lang',methods=['POST'])
    def addOne():
        language = {'name': request.json['name']}
        languages.append(language)
        return jsonify({'languages':languages})

In Postman, we set url http://127.0.0.1:8080/lang/ and body

    { "name": "Go" }

Will show

    {
        "languages": [
            {
                "name": "JavaScript"
            },
            {
                "name": "Python"
            },
            {
                "name": "Ruby"
            },
            {
                "name": "Go"
            }
        ]
    }

## PUT Request

** Modify a language **

    @app.route('/lang/<string:name>', methods=['PUT'])
    def editOne(name):
        langs = [language for language in languages if language['name'] == name]
        langs[0]['name'] = request.json['name']
        return jsonify({'language': languages})

In Postman, we set url http://127.0.0.1:8080/lang/JavaScript and body

    { "name": "Go" }

Will show

    {
        "languages": [
            {
                "name": "Go"
            },
            {
                "name": "Python"
            },
            {
                "name": "Ruby"
            },
        ]
    }

## DELETE Request

** Delete a language **

    @app.route('/lang/<string:name>', methods=['DELETE'])
    def removeOne(name):
        langs = [language for language in languages if language['name'] == name]
        languages.remove(langs[0])
        return jsonify({'language': languages})

In Postman, we set url http://127.0.0.1:8080/lang/JavaScript

Will show

    {
        "languages": [
            {
                "name": "Python"
            },
            {
                "name": "Ruby"
            },
        ]
    }

## Conclusion

These four methods are the commonly used function, we can learn how to build Bsic RESTful API. However, this practice still have to connect to MySQL or MongoDB to make it more practical. So, let's hurry up to try connecting to database!

