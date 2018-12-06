# docker-nginx-redirect

A very simple container to redirect HTTP traffic to another server, based on `nginx`

## Resources

- [Docker Hub](https://hub.docker.com/r/platohq/nginx-redirect/)

## Configuration

### Environment variables

| SERVER_REDIRECT           | Server to redirect to                                                                                                                                                                                                                                                            | www.example.com           |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| SERVER_NAME               | Optionally define the server name to listen on, it is useful for capturing variable to use in server_redirect.                                                                                                                                                                   | `~^www.(?.+).example.com` |
| SERVER_REDIRECT_PATH      | Optionally define path to redirect all requests eg. `/landingpage`, if not set nginx var `$request_uri` is used                                                                                                                                                                  |                           |
| SERVER_REDIRECT_SCHEME    | Optionally define scheme to redirect to, if not set nginx var `$scheme` is used                                                                                                                                                                                                  |                           |
| SERVER_REDIRECT_CODE      | Optionally define the http status code to use for redirection, if not set or not in list of allowed codes 301 is used as default, allowed codes are: 301, 302, 303, 307, 308                                                                                                     |                           |
| SERVER_REDIRECT_POST_CODE | Optionally define the http code to use for POST redirection, useful if client should not change the request method from POST to GET, if not set or not in allowed codes `SERVER_REDIRECT_CODE` is used, so per default all requests will be redirected with the same status code |                           |
| SERVER_ACCESS_LOG         | Optionally define the location where nginx will write its access log,if not set `/dev/stdout` is used                                                                                                                                                                            |                           |
| SERVER_ERROR_LOG          | Optionally define the location where nginx will write its error log, if not set `/dev/stderr` is used                                                                                                                                                                            |                           |

## Usage

    docker run -e SERVER_REDIRECT=www.example.com -p 8888:80 platohq/nginx-redirect
    docker run -e SERVER_REDIRECT=www.example.com -e SERVER_REDIRECT_PATH=/landingpage -p 8888:80 platohq/nginx-redirect
    docker run -e SERVER_REDIRECT=www.example.com -e SERVER_REDIRECT_PATH=/landingpage -e SERVER_REDIRECT_SCHEME=https -p 8888:80 platohq/nginx-redirect

