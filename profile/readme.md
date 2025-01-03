# Scraper

## Table of content

1. [Introduction](#introduction)
2. [Software components](#software-components)
3. [Technical stack](#technical-stack)
4. [How to run tests](#how-to-run-tests)
5. [Pre-requisites to build and run](#pre-requisites-to-build-and-run)
3. [How to build and run](#how-to-build-and-run)

## Introduction

This is a scraper which can use to submit a valid URL and scrape following information from the website content.

* HTML version
* Page title
* Number of headings and levels
* Internal links
* External links
* Number of inaccessible links on the page
* If the page contains a login form

## Software components

1. [Scraper client](https://github.com/go-scraper/scraper-client) - This is the client facing web application which can access through the browser. This connects with the Scraper API to execute scraping.
2. [Scraper API](https://github.com/go-scraper/scraper-api) - This is the backend API service for the scraper client web application. This executes the scraping and responds back to the web application with the information found.

## Technical stack

### Scraper API

1. Go language
2. Gin framework
3. Monkey mock
4. Httpmock
5. Testify
6. Cors
7. Docker
8. Docker compose
9. Github actions
10. Go vet

### Scraper client

1. ReactJs
2. TypeScript
3. Material UI
4. Docker
5. Docker
6. Docker compose
7. Github actions

## How to run unit tests

### 1. Scraper API

#### Pre-requisites

* Go lang

#### Steps

1. Clone the github repo using, `git@github.com:go-scraper/scraper-api.git` command.
2. Open the command line and navigate to the `scraper-api` dir.
3. Run `go mod tidy` command to install all dependencies listed in `go.mod` file.
4. To run unit tests with the coverage output run `go test -coverprofile=coverage.out ./...` command.
5. To view the test coverage run `go tool cover -func=coverage.out` command.

![Test coverage output](../resources/test_coverage_output.png)

## Pre-requisites to build and run

* Docker - Since both software components are Dockerized, having docker service up and running on your machine would be enough to build and run the scraper.

## How to build and run

To use the scraper, we have to run both scraper client and the API.

### 1. Scraper API - [GitHub repo](https://github.com/go-scraper/scraper-api)

1. Clone the github repo using, `git@github.com:go-scraper/scraper-api.git` command if you haven't already.
2. Open the command line and navigate to the root folder `(scraper-api)` of the project.
3. To build and run with the docker run `docker-compose up --build` command.
4. Try sending a `GET` request using Postman or any client to the URL `http://localhost:8080/scrape?url=https://google.com`. You can have any valid URL to the `url` query parameter.
5. If the application is up and running without any errors, you should receive a response in below format with the HTTP code `200`.

```json
{
    "request_id": "20250104020245-hYVHLDhl",
    "pagination": {
        "page_size": 10,
        "current_page": 1,
        "total_pages": 2,
        "next_page": "/scrape/20250104020245-hYVHLDhl/2"
    },
    "scraped": {
        "html_version": "HTML 5",
        "title": "Google",
        "headings": {},
        "contains_login_form": false,
        "total_urls": 19,
        "internal_urls": 15,
        "external_urls": 4,
        "paginated": {
            "inaccessible_urls": 0,
            "urls": [
                {
                    "url": "https://www.google.com/imghp?hl=en&tab=wi",
                    "http_status": 200,
                    "error": ""
                },
            ]
        }
    }
}
```

6. Next we should build and run the Scraper client application.

### 2. Scraper client - [GitHub repo](https://github.com/go-scraper/scraper-client)

1. Clone the github repo using, `git clone git@github.com:go-scraper/scraper-client.git` command if you haven't already.
2. Open the command line and navigate to the root folder `(scraper-client)` of the project.
3. To build and run with the docker run `docker-compose up --build` command.
4. Access the web application on your browser using the `http://localhost:3000/` URL.

![Client empty screen](../resources/client_empty_screen.png)
[Figure 01 - Client application screen]

5. Now you can enter a URL on the input box and click on `SCRAPE` button or hit `Enter`. You should see the scraping result as below screenshot.

![Client result screen](../resources/client_result_screen.png)
[Figure 02 - Client application screen with scraping results]