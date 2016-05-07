---
inFeed: true
hasPage: true
inNav: false
inLanguage: null
keywords: []
description: ' '
datePublished: '2016-05-07T04:13:40.368Z'
dateModified: '2016-05-07T04:13:38.047Z'
title: ''
author: []
sourcePath: _posts/2016-05-07-access-bitbucket-repo-from-within-a-meteor-app.md
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: true
url: access-bitbucket-repo-from-within-a-meteor-app/index.html
_type: Article

---
****

**Access BitBucket repo from within a Meteor app**

I'm thinking of creating an app that creates apps, using Meteor.

So I need to be able to create a new repo for every user who wants to create a new app. Therefore, I need to be able to access BitBucket and create / update a repo with all the code needed to maintain that app.

For 2 weeks now, I've struggled to find a way to access my own BitBucket account in order to programmatically add / update new repo's.

Today, just after my tweet, I got it to work by adding a nodejs package to my admin app.

Here's what I did:

meteor add meteorhacks:npm

(Yes, I'm not up to Meteor 1.3 just yet - it has true NPM support)

In the packages.json folder in the root of my project, I added this:

{ "node-bitbucket-api" : "0.1.0" }

In my source, I added this:

var bitbucket = Meteor.npmRequire('node-bitbucket-api');   
var credentials = {username: 'USER', password: 'PWD'};   
var client = bitbucket.createClient(credentials);   
var repository = client.getRepository({slug: 'SLUG', owner: 'OWNER'}, function (err, repo) { console.log(JSON.stringify(repo); });

And it worked - I got a JSON response back that identified my chosen repo.

No mucking about with oAuth etc - just using my standard login credentials.

So, baby steps, but so far advanced as to where I was 2 weeks ago!

I just love this Meteor platform - \#meteorjs ![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/2afa66c8-d308-49bb-8f94-641a8e71d3cd.png)