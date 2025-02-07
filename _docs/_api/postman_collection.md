---
nav_title: Sample Requests
platform: REST APIs
page_order: 3
search_rank: 5
---

# Sample API Requests

Braze allows you to generate sample API requests for all of our endpoints via our Postman Collection.

## What is Postman?

Postman is a free-to-use visual editing tool for building and testing API requests. As opposed to other methods for interacting with APIs (e.g. using cURL), Postman allows you to easily edit API requests, view header information, and much more. Postman has the ability for you to save Collections or libraries of sample premade API requests. To make it easy for our customers to get up and running with our REST API, we created a Collection with premade examples for all of our API endpoints.

## Downloading Postman

Postman has MacOS, Windows, and Linux versions can be downloaded from their website located [here][1].

## Getting the Braze Postman Collection

The Braze Postman Collection can be added to your local Postman app by doing the following:

1. Open the app and click the the "Import" button in the upper left corner.
2. Within the modal window that opens, select the "Import from Link" option
3. Copy and paste this URL `https://www.getpostman.com/collections/5a6394e1ba47f013cdc9` and click "Import".

## Setting up your Postman Environment

The Braze Postman Collection uses a templating variable, `{{instanceURL}}`, to substitute the REST API URL of your Braze instance into the pre-built requests. Rather than having to manually edit all requests in the Collection, you can set up this variable in your Postman environment. To do so, please follow the steps below:

1. Click on the gear icon in the top right corner of the Postman app. ![Managing Environments][2]{: height="40%" width="40%"}
2. Select "Manage Environments" to open a modal window which displays your active environments.
3. In the bottom right corner of the modal window, click "Add" to create a new environment.
4. Give this environment a name (e.g. "Braze API Requests") and add keys for `instance_url` and `api_key` with values corresponding to your Braze REST API URL and Braze REST API Key as pictured below. The `api_key` should be encapsulated in quotes.
  - The value that you need to add for `instance_url` is dependent on your Braze instance. For more information, please see our [Rest API "Endpoint" documentation.][7]
  - For more information on your `api_key` please see our ["App Group REST API Key" documentation.][8]

![Adding environment variables][3]

## Using the pre-built requests from the Collection

Once you have configured your environment. You can use any of the pre-built requests in the collection as a template for building new API requests. To start using one of the pre-built requests, simply click on it within the 'Collections' menu on the left side of Postman. This will open the request as a new tab in the main window of the Postman app.

In general, there are two types of requests that Braze's API endpoints accept - `GET` and `POST`. Depending on which HTTP method the endpoint uses, you'll need to edit the pre-built request differently.

### Editing a POST request

When editing a `POST` request, you'll need to open the request and navigate to the 'Body' section in the request editor. For readability, select the `raw` radio button to format the JSON request body.

![Editing a POST request][4]

### Editing a GET request

When editing a `GET` request, you will need to edit the parameters passed in the request URL. To edit these easily, select the 'Params' button next to the URL bar and edit the key-value pairs in the fields that will appear below the URL bar.

![Editing a GET request][5]

## Sending your request and viewing the response data

Once your API request is ready to send, click on the 'Send' button next to the URL bar. The request will be sent and the response data will be populated in a section underneath the request editor. From here, you can view the raw data returned from Braze's API, see the HTTP response code, see how long the request took to process, and view header information.

![Response Data][6]

[1]: https://www.getpostman.com
[2]: {% image_buster /assets/img_archive/postman_environments.png %}
[3]: {% image_buster /assets/img_archive/postman_variable.png %}
[4]: {% image_buster /assets/img_archive/postman_post.png %}
[5]: {% image_buster /assets/img_archive/postman_get.png %}
[6]: {% image_buster /assets/img_archive/postman_response.png %}
[7]: {{ site.baseurl }}/developer_guide/rest_api/basics/#endpoints
[8]: {{ site.baseurl }}/developer_guide/rest_api/basics/#app-group-rest-api-keys
