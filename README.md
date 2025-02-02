> **Note**: This repo is no longer officially maintained as of Jan, 2023.
> Feel free to use it, fork it and patch it for your own needs.

[![CircleCI](https://img.shields.io/circleci/project/github/contentful/the-example-app.csharp.svg)](https://circleci.com/gh/contentful/the-example-app.csharp)

## The ASP.NET example app

The ASP.NET example app teaches the very basics of how to work with Contentful:

- consume content from the Contentful Delivery and Preview APIs
- model content
- edit content through the Contentful web app

The app demonstrates how decoupling content from its presentation enables greater flexibility and facilitates shipping higher quality software more quickly.

<a href="https://the-example-app-csharp.herokuapp.com/" target="_blank"><img src="https://images.contentful.com/88dyiqcr7go8/50rjTJcWm4wAuW8AQwIQeI/37a924b510db89d228b4214f8508829c/the-example-app-csharp.herokuapp.com.png" alt="Screenshot of the example app"/></a>

You can see a hosted version of `The ASP.NET example app` on <a href="https://the-example-app-csharp.herokuapp.com/" target="_blank">Heroku</a>.

## What is Contentful?
[Contentful](https://www.contentful.com) provides a content infrastructure for digital teams to power content in websites, apps, and devices. Unlike a CMS, Contentful was built to integrate with the modern software stack. It offers a central hub for structured content, powerful management and delivery APIs, and a customizable web app that enable developers and content creators to ship digital products faster.

## Requirements

* .NET Core
* Git
* Contentful CLI (only for write access)

Without any changes, this app is connected to a Contentful space with read-only access. To experience the full end-to-end Contentful experience, you need to connect the app to a Contentful space with read _and_ write access. This enables you to see how content editing in the Contentful web app works and how content changes propagate to this app.

## Common setup

Clone the repo and install the dependencies.

```bash
git clone https://github.com/contentful/the-example-app.csharp.git
```

```bash
dotnet restore
```

## Steps for read-only access

To start the server, run the following

```bash
dotnet run
```

Open [http://localhost:3000](http://localhost:3000) and take a look around. 


## Steps for read and write access (recommended)

Step 1: Install the [Contentful CLI](https://www.npmjs.com/package/contentful-cli)

Step 2: Login to Contentful through the CLI. It will help you to create a [free account](https://www.contentful.com/sign-up/) if you don't have one already.
```
contentful login
```
Step 3: Create a new space
```
contentful space create --name 'My space for the example app'
```
Step 4: Seed the new space with the content model. Replace the `SPACE_ID` with the id returned from the create command executed in step 3
```
contentful space seed -s '<SPACE_ID>' -t the-example-app
```
Step 5: Head to the Contentful web app's API section and grab `SPACE_ID`, `DELIVERY_ACCESS_TOKEN`, `PREVIEW_ACCESS_TOKEN`. 

Step 6: Open `appsettings.json` and inject your credentials like this.

```
{
  "ContentfulOptions": {
    "DeliveryApiKey": "<DELIVERY_ACCESS_TOKEN>",
    "PreviewApiKey": "<PREVIEW_ACCESS_TOKEN>",
    "SpaceId": "<SPACE_ID>",
    "UsePreviewApi": false
  }
}
```

Step 7: To start the kestrel server, run the following
```bash
dotnet run
```
Final Step:

Open [http://localhost:3000?editorial_features=enabled](http://localhost:3000?editorial_features=enabled) and take a look around. This URL flag adds an “Edit” button in the app on every editable piece of content which will take you back to Contentful web app where you can make changes. It also adds “Draft” and “Pending Changes” status indicators to all content if relevant.

## Deploy to Heroku
You can also deploy this app to Heroku:

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Deploy to Azure
You can also deploy this app to Azure:

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

