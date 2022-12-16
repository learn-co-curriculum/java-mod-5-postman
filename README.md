# Introduction to Postman

## Learning Goals

- Install the Postman API client tool.
- Compose a request with a URL, HTTP verb, headers, and body
- Test GET, POST, PUT, and DELETE requests using Postman.

## Introduction

When developing a web application, our primary goal is to take an
**HTTP request** and return an appropriate **response**, following the idea of
**client-server** communication. So far, we've been using one particular client
to interact with our server: the browser!

It's straightforward to use the browser to make a GET request — all we
have to do is enter an address in the browser's URL bar, such as
`http://localhost:8080/greet`, and hit enter.

However, we will be writing web applications that use other HTTP verbs aside from `GET`,
such as `POST`, `PUT`, and `DELETE`. Using these other HTTP verbs is a strong
convention when working with APIs in particular: they signal to developers that
the server is going to perform a specific kind of action, based on which HTTP
verb is used in the request:

- **POST** (Create): create a new resource
- **GET** (Read): access/query information
- **PUT** (Update): update a specific resource
- **DELETE** (Delete): delete a specific resource

Luckily for us, there are some excellent tools out there to make it easy to interact
with APIs and customize all different parts of the request (the headers, HTTP
verb, URL, and body).

## Using Postman as an API Client

The tool we'll be demonstrating in this lesson is [Postman][]. Postman is an API
Client tool that will help with testing and development of our API.

First, head to this page and download Postman:
[https://www.postman.com/downloads/][postman download]. Make sure to download
the app rather than use the web version. If you have any issues downloading,
make sure to check out the [Postman docs][] for help.

After downloading, run the installer.  You can create a free account or skip that step
and go straight to the app. You should see a screen like this (version may differ):

![postman welcome screen](https://curriculum-content.s3.amazonaws.com/phase-4/testing-apis-with-postman/postman-welcome-screen.png)

## JSON Placeholder API

To show what we can do with Postman, we're going to be using the
[JSON Placeholder API][json placeholder], a free resource where we can try out
different requests. 

You can see the various resources available at [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/)
(scroll down to "Resources").

![JSON Placeholder Resources ](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/jsonplaceholder_resources.png)  

Let's explore the `posts` resource, which represents a collection of
blog posts (not to be confused with the HTTP POST verb).
Clicking on the [/posts](https://jsonplaceholder.typicode.com/posts) link returns
a JSON object containing a list of blog posts:

```xml
[
        {
        "userId": 1,
        "id": 1,
        "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
        "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
        },
        {
        "userId": 1,
        "id": 2,
        "title": "qui est esse",
        "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
        },
        {
        "userId": 1,
        "id": 3,
        "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
        "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
        },
...
]
```

Scroll down further on [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/) to
see the routes available for testing.  Each route represents a path.  We use the combination of an HTTP verb
and a route to perform an action, such as getting a blog post or deleting a blog post.  

![JSON placeholder routes](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/jsonplaceholder_routes.png)

## GET request in Postman

For our first request, we'll make a simple GET request to
`https://jsonplaceholder.typicode.com/posts/1`.

Click on the plus sign in Postman to open a new tab. 

![new tab postman](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/new_request.png)

You should see a field where you can enter your request.
Enter the URL `https://jsonplaceholder.typicode.com/posts/1` in the field and click send:

![postman_request_url](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/new_request_url.png)


The request is sent to the server and a response is generated and returned to Postman.
Notice the HTTP status response code is `200`. The HTTP 200 OK success status
response code indicates that the request has succeeded.

![postman get request response](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/get_request_response.png)

We receive a JSON object as a response, which is the blog post with id `1`:

```json
{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

## POST request in Postman

The HTTP verb `GET` was used to retrieve an existing blog post.  We will use the
HTTP verb `POST` to create a blog post.  Note that [JSON Placeholder API][json placeholder]
does not actually store the new blog post anywhere, it just returns a response pretending
it did.

First, update the **URL** to be `https://jsonplaceholder.typicode.com/posts`
(remove the id value of `1`). Then, click the dropdown next to the URL bar,
and change the **HTTP verb** from a `GET` request to a `POST` request.

In previous lessons  we sent request data through
the URL either in the query string or as path parameters when we made a GET request.
However, a POST request typically sends data through the request
body, thus the data is not part of the URL.

Thus, we need some way of sending a JSON formatted string in the **body**
of the request. Click the 'Body' tab in Postman, then click the dropdown and
select 'raw' to specify that we are sending a raw string of data. Then, select
JSON from the next dropdown to specify that the string will be formatted as
JSON. 

![post request in postman](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/post_request.png)

Now we can add a JSON formatted string to the text area below the
dropdown:

```json
{
  "title": "testing post request",
  "body": "blah blah blah blah .......",
  "userId": 1
}
```

> **Note**: for the string to be considered valid JSON, all the keys on the
> object must be in **double-quotes**. There also can't be any trailing commas
> after the last key-value pair. You can use [this JSON tool][json lint] to
> validate your JSON if you need to troubleshoot.

With all that in place, click send.

Success! The API has received our request and sent back a response representing
a newly created `post` with id `101`:

```json
{
  "title": "testing post request",
  "body": "blah blah blah blah .......",
  "userId": 1,
  "id": 101
}
```

You'll also notice some additional info comes back in the response, such as a
status code of `201 Created` that indicates the successful creation of a
resource.

![post request response](https://curriculum-content.s3.amazonaws.com/6036/java-mod-5-postman/post_request_response.png)

Experiment with Postman by making requests to other endpoints for the
[JSON Placeholder API][json placeholder]. Try making a PUT request and a
DELETE request. What changes between these different requests? What does this
API send as a response if you make a bad request?

## Conclusion

API clients like Postman are extremely valuable to have in your API developer
toolkit. They make it simple to interact with servers by giving you full control
over how the response is being sent, with a nice interface for customizing the
HTTP verb, URL, headers, and body.

In future lessons, we'll be expanding our API to handle non-GET requests, so
being able to use a tool like Postman will make our API development much easier!
It's also a great tool to use if you're exploring a third-party API for use in
your projects.

## Resources

- [Postman Documentation][postman docs]

[postman]: https://postman.com
[postman download]: https://www.postman.com/downloads/
[postman docs]: https://learning.postman.com/docs/getting-started/installation-and-updates/
[json placeholder]: https://jsonplaceholder.typicode.com/guide/
[json placeholder resources]: https://jsonplaceholder.typicode.com/
[json lint]: https://jsonlint.com/
