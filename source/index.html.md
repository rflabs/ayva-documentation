---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - java
  - python

toc_footers:
  - <a href='https://github.com/rflabs/ayva'>Ayva Library</a>
  - <a href='https://github.com/rflabs/ayva-cli'>Ayva CLI</a>

includes:
  - errors

search: true
---

# Introduction

Ayva is an open-source cross-platform developer framework used to build voice assistant apps. The features and tools provided in this framework are platform agnostic, allowing developers to build once and deploy on both Google Assistant and Alexa. 

<b>The Ayva framework is built up of the following:</b>

* Ayva Library
* Ayva CLI
* Middleware tools

<b>Benefits</b>

* No need to manually define the interaction model in every AI platform.
* Voice app will have the same interaction model (user experience) across all voice assistants.

## Architecture

![ayva-architecture](https://storage.googleapis.com/ayva-helloworld.appspot.com/ayva-architecture-v2.png)

<aside class="notice">
Currently only avalable on Node.js
</aside>

# Setup

In order to fully experience Ayva's end-to-end development process, some prerequisite setup is required. 

<b>All</b>

* [Ayva CLI](https://www.npmjs.com/package/ayva-cli)
* [Bespoken](https://bespoken.io/bst/)

<b>Amazon Alexa</b>

* [Amazon developer account](https://developer.amazon.com/)
* [Amazon Ask command line interface (CLI)](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)
* [Alexa skill id](https://developer.amazon.com/edw/home.html#/skill/create/)


<b>Google Assistant (Dialogflow)</b>

* [Dialogflow developer account](https://console.dialogflow.com/api-client/#/login)
* [Dialogflow agent developer id](https://console.dialogflow.com/api-client/#/newAgent)

## Ayva CLI

</br>

> Global npm install of Ayva command line interface

```javacript
npm install -g ayva-cli
```

<b>1. Install [Ayva CLI](https://www.npmjs.com/package/ayva-cli)</b>

<code>npm install -g ayva-cli</code>

The Ayva CLI will allow you to create new voice assistant projects and deploy interaction models to any supported voice assistant platform. 

</br>

> Global npm install of Bespoken CLI tools

```javacript
npm install -g bespoken-tools
```

<b>2. Install [Bespoken CLI tools](https://www.npmjs.com/package/bespoken-tools)</b>

<code>npm install -g bespoken-tools</code>

The <code>Ayva deploy</code> command in our CLI utilizes [Bespoken](https://bespoken.io/bst/) to create a local proxy url. This greatly increase the efficiecy of local development. Using a local proxy avoids the necessity to deploy your code on every update.

## Amazon Alexa

</br>
<b>1. Create a [Amazon developer account on Amazon](https://developer.amazon.com/)</b>

</br>

> Global npm install of Amazon Ask CLI

```javascript
npm install -g ask-cli
```

<b>2. Install [Amazon Ask command line interface (CLI)](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)</b>

<code>npm install -g ask-cli</code>

(If you're using Linux, the installation my require <code>sudo</code>)

</br>

> Initialize Amazon developer account credentials

```javascript
ask init
```

<b>3. Initialize Ask CLI with your Amazon developer account credentials</b>

The first time you use this CLI, you must call the <code>init</code> command to initialize the tool with your Amazon developer account credentials.

<code>ask init</code>

You will be prompted to name your profile (default by default), choose the AWS profile to use, and to log in to your Amazon developer account. Once the initialization is complete, you can use ASK CLI to manage your skill.

</br>
<b>4. Create a new Alexa skill with [Alexa skills kit](https://developer.amazon.com/edw/home.html#/skill/create/)</b>

In order to utilize <code>Ayva deploy</code>, you will need to first create a new Alexa skill to obtain your <b>Alexa Skill Id</b>. This is what Ayva will use to configure the interaction model for your voice assistant app.

![alexa-id](https://storage.googleapis.com/ayva-helloworld.appspot.com/alexa-id-v3.png)

## Dialogflow (Google)

</br>
<b>1. Create a [Dialogflow developer account](https://console.dialogflow.com/api-client/#/login)</b>

</br>
<b>2. Create a [new Dialogflow agent](https://console.dialogflow.com/api-client/#/newAgent)</b>

Ayva currently uses [Dialogflow V1 API](https://dialogflow.com/docs/reference/agent/). In order to utilize <code>Ayva deploy</code>, you will need to first create a new Dialogflow agent to obtain your <b>Developer access token</b>. This is what Ayva will use to configure the interaction model for your voice assitant app.

![df-devToken](https://storage.googleapis.com/ayva-helloworld.appspot.com/df-devToken.png)

# Hello Ayva

This section will explain how to locally deploy and interact with our 'Hello Ayva' voice app on your own voice assitant device. 

This tutorial will walk you through the basic commands in the Ayva CLI to guide you through each phase of the development and release process. After this tutorial, you will know how to use the Ayva library to build your very own voice app.

## Prerequisites

Please follow the instructions in Setup before continuing. If you'd like to deploy on both Alexa and Google Assistant, please ensure you complete all the requirements outined in the previous section. 

<b>Any</b>

* [Ayva CLI](https://www.npmjs.com/package/ayva-cli)
* [Bespoken](https://bespoken.io/bst/)

<b>Amazon Alexa</b>

* [Amazon developer account](https://developer.amazon.com/)
* [Amazon Ask command line interface (CLI)](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)
* [Alexa skill id](https://developer.amazon.com/edw/home.html#/skill/create/)


<b>Google Assistant (Dialogflow)</b>

* [Dialogflow developer account](https://console.dialogflow.com/api-client/#/login)
* [Dialogflow agent developer id](https://console.dialogflow.com/api-client/#/newAgent)


## Create

> Clone 'Hello Ayva' app and configure voice assistant credentials

```javascript
ayva create
```

<code>ayva create</code>

This command will clone our 'Hello Ayva' app into the folder this command was run in, as well as capture the necessary information to push the app's interaction model to the selected voice asssitant platform.

![ayva-create](https://storage.googleapis.com/ayva-helloworld.appspot.com/ayva-create-v2.png)

> Alexa config that will be generated in ayva.json

```javascript
{"invocationPhrase":"hello ayva",
  "alexa": {
    "skillId":"<Alexa skill id>"}
  }
}
```
### Alexa skill id

Alexa configuration requires the developer define the Alexa skill id and the skill's invocation name. We recommend using the name of your application as the invocation name (i.e 'Hello Ayva' in this tutorial)

![alexa-step1](https://storage.googleapis.com/ayva-helloworld.appspot.com/alexa-step1.png)

> Dialogflow config that will be generated in ayva.json

```javascript
"dialogflow":{
  "developerAccessToken":"<agent developer access token>"
},
```

### Dialogflow Developer Access Token

Dialogflow configuration requires the developer define the Dialogflow agent id.

![df-step1](https://storage.googleapis.com/ayva-helloworld.appspot.com/df-step1.png)

![df-step2](https://storage.googleapis.com/ayva-helloworld.appspot.com/df-step2.png)


## Deploy


## Run


# Ayva Library Reference

## Initialization

## State management

## Speech Models

## Intents

## Error Handling


# Ayva CLI Reference

## create

## deploy

## run

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve


```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

