# Link Shortener

## Setup

- `bundle install`
- `cd client/ && npm install && cd ..`
- `rails db:create && rails db:schema:load`
- `rails start`

## create a link
```
POST /short_link CONTENT-TYPE application/json
{
  "long_url": "<long_url>"
}
RESPONSE
{
  "long_url": "<long_url>",
  "short_link": "<short_link>"
}
```

- The long_url should be a valid URL like https://kapost.com.
- If the long_url has already been shortened, you should return the previously created
short_link.
- Otherwise, you should return a new short_link.
- short_link should look something like http://localhost:8080/a1B2c3D4

## Accessing a Short Link
Once you have a generated short link, you should be able to access the short link and
be redirected to the long link (original URL). The request would look something like
GET http://localhost:8080/a1B2c3D4

which would return a 301 that redirects the user to the original URL.


## Bonus Points
If you have time, you could create an analytics view for a given short link that will show
analytics about each time the short link has been accessed. The analytics view is
signified by adding a + to the end of a given short link. For example

```
GET http://localhost:8080/a1B2c3D4+
{
  "response": [
    {
      "time": "2018-10-01T10:00:00Z",
      "referrer": "none",
      "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
    },
    {
      "time": "2018-10-01T15:30:10Z",
      "referrer": "none",
      "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
    }
  ]
}
```

In the above example, the referrer is none because the link was directly pasted into a
browser. It should follow the same semantics of the HTTP referrer header.

## Testing

`rspec`
