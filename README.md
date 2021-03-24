# A link shortening service

> API to create short urls using Node, Express and MongoDB

## Quick Start

```bash
# Install dependencies
npm install

# Edit the default.json file with your mongoURI and baseUrl

# Run
npm start
```

## Launch the application (http://localhost:5000/)
1. Enter the Url in the text field, and click Shorten Url
2. Click the valid shorten Url response


## Conceptual Questions

```
1. How would you test this service?

Launch the application and enter the URL in the text field. If the text field is empty or the URL entered is not valid, application shows the error. Once if the valid URL is entered, Click on the Shorten Url button, it responds back with the shortened Url. Click on the Url which responded on the screen. It will be redirected to the Url that is entered.

```

```
2. What DB models would need to change to support multiple users?

If we need to support multiple users to the application, We can add a user DB model with fields namely UserId, UserName, and any other fields. And there seems to be only one relationship between the two records, which is to store the which user has created the URL. So we can add UserId to the existing Url model.

```

```
3. How can this service support 1000 concurrent requests?

Inorder to support 1000 concurrent requests or more, this service can be implemented with the following modules.

1. We can use either a elastic load balancer or auto balancer that sends the request to the multiple servers.

2. Cluster of id generators can be managed using the distributed system that is assigned to each user to assign the id generated (for shortid) from the each system that reduces the concurrency.

3. Also, we can use the cache system for faster retrieval that also reduces the database calls.

```

## Architecture

![DS](https://user-images.githubusercontent.com/26082173/112240295-d24f7280-8c26-11eb-96c4-3562caf2018a.png)

```
4. What kind of database models do you think would cause an issue? And why?

Url database model would cause an issue. Because, if two users request the shorten url at the same time, there is chance of the storing the duplicate code as I am using the base62 encoding shortid. This results in a concurrency issue.

```

```
5. Which parts of the service do you think are most likely to fail? And why?

If two different url has the same short id which is encoded with the base62 could result in the key duplication in the database. So, It will not return the valid response.

```
