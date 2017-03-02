---
layout: post-index
date: 2017-02-27
img: 
alt: image-alt
tag: [AWS,Python]
category: [Data wrangling]
comments: true
---
One of my side projects is the creation of a "serverless" race track directory application. The back-end consists
of race track microservice utilizing the AWS API Gateway, Lambda, and DynamoDB products. In this post I am using 
the Python language to transform an existing dataset into a format that can be used with DynamoDB and load the
data to the DynamoDB table via the API.

The following JSON is the existing format the data is in. It was created prior to the selection of the back-end
and needs to be flattened to work with the DynamoDB table.

{% highlight javascript %}
  {
    "name": "Red Rock Raceway",
    "trackDetails": {
      "type": "Oval",
      "length": "1/8 Mile",
      "surface": "Dirt / Clay",
      "gps": {
        "lat": 40.250382,
        "lon": -78.565072
      }
    },
    "contact": {
      "address": {
        "street": "555 Deichland Road",
        "city": "Claysburg",
        "state": "PA",
        "zip": "16625"
      },
      "contactName": "Troy Aikey",
      "phone": "814-285-2077",
      "email": "",
      "website": "http://www.redrockraceways.com/",
      "social": {
        "facebook": "https://www.facebook.com/Red-Rock-Raceways-215083415336098/",
        "twitter": "",
        "googleplus": ""
      }
    },
    "logoImage": "TrackImages/RedrockRacewaysLogo.png"
  }
  {% endhighlight %}

Below is the new desired format. Notice all empty strings are null since DynamoDB would not accept an empty string. 

{% highlight javascript %}
{
  "surfaceType": "Dirt / Clay",
  "primaryContact": "Troy Aikey",
  "lon": -78.565072,
  "lat": 40.250382,
  "street": "555 Deichland Road",
  "zip": "16625",
  "name": "Red Rock Raceway",
  "state": "PA",
  "primaryEmail": null,
  "facebook": "https://www.facebook.com/Red-Rock-Raceways-215083415336098/",
  "trackLogoURL": null,
  "length": "1/8 Mile",
  "websiteURL": "http://www.redrockraceways.com/",
  "city": "Claysburg",
  "primaryPhone": "814-285-2077",
  "type": "Oval",
  "twitter": null
}
{% endhighlight %}

*Transformer
This is my first practical usage of the Python. In the past I've used java and groovy for transforming data in
code based solutions. The script below reads in the existing Tracks.json dataset, transforms each of the track 
objects to the new format, and writes out a new JSON to the NewTracks.json file. 

{% highlight python %}
import json

with open('Tracks.json') as data_file:
    data = json.load(data_file)
    output = []
    for track in data :
        twitter = track['contact']['social']['twitter']
        if not twitter:
            twitter = None

        primaryContact = track['contact']['contactName']
        if not primaryContact:
            primaryContact = None

        primaryEmail = track['contact']['email']
        if not primaryEmail:
            primaryEmail = None

        facebook = track['contact']['social']['facebook']
        if not facebook:
            facebook = None

        primaryPhone = track['contact']['phone']
        if not primaryPhone:
            primaryPhone = None

        d =  {
            'facebook': facebook,
            'zip': track['contact']['address']['zip'],
            'lon': track['trackDetails']['gps']['lon'],
            'primaryPhone': primaryPhone,
            'name': track['name'],
            'state': track['contact']['address']['state'],
            'city': track['contact']['address']['city'],
            'twitter': twitter,
            'length': track['trackDetails']['length'],
            'websiteURL': track['contact']['website'],
            'surfaceType': track['trackDetails']['surface'],
            'primaryContact': primaryContact,
            'lat': track['trackDetails']['gps']['lat'],
            'primaryEmail': primaryEmail,
            'trackLogoURL': None,
            'type': track['trackDetails']['type'],
            'street': track['contact']['address']['street']
        }
        output.append(d)
with open('NewTracks.json', 'w+') as f:
  json.dump(output, f, ensure_ascii=False)
{% endhighlight %}