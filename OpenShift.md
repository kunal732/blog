Using Openshift As MBaaS
==

![Figure 1-1](http://s16.postimg.org/nm6afhz11/mobile.jpg "Figure 1-1")

Are you in the process of building a mobile app or have created one in which you require some information or data to be stored off device ? Do you need a server side component to store stats, high scores maybe even location-based information. Perhaps you have users that need to interact with each other. In instances like this it makes life a lot easier to take advantage of what’s known as a Mobile Backend as a Service (MBaaS). Certainly there are situations in which you can have applications that can be self contained such as the calculator app but most modern apps are not going to be like that. 

There are multiple services that not only help solve these problems but also auto scale based on load. The one I've been playing around with recently is Redhat's OpenShift platform. I think the service is interesting since it wasn't designed to specifically be a MBaaS, but has this concept of quickstarts and cartridges that let it become extendable and take on new functionality. 


What do I look for in a Backend:
---------
#####Storage of Custom Objects: 
Due to the nature of Objective-C, you typically have objects that represent some type of information. So relational DB’s while usable are not ideal. Mongo makes sense for storage but for a Mobile Backend you want the process of storing and retrieving to be easy. 
That’s why I like the integration OpenShift has with MongoLabs. They provide an API layer over MongoDB that makes it easy to communicate from my mobile device without having to create my own custom APIs. 
The MongoLabs OpenShift Quickstart can be found here: https://github.com/mongolab/mongolab-openshift-quickstart. 
Documentation on the APIs that MongoLabs makes available is located here, https://support.mongolab.com/entries/20433053-Is-there-a-REST-API-for-MongoDB-


#####Spatial/Geo Support: 
The apps I see that take the best advantage of a MBaaS usually have a location based component. It’s useful to perform searches on objects near a particular location. With MongoDB and the MongoLabs API this becomes very easy to implement. 
```
POST
https://api.mongolab.com/api/1/databases/mbaas/geomail
 
data: { "email" : "kunal@sendgrid.com",
        "location" : { "lat" : 40, "long" : 73 } }
 
GET
https://api.mongolab.com/api/1/databases/mbaas/geomail?q={"location":{"$near":{"lat":40,"long":73}}}
```

#####Strong 3rd Party service integration: 
The other aspect of what makes Redhat an interesting choice is the abundance of quick starts / cartridges to quickly use 3rd party apis and integrate their services quickly into your backend. With a quick RHC command line script I can quickly setup very useful applications without having to worry about environment or dependency issues. 

Real Time Push Notifications:

- Pusher: (https://www.openshift.com/quickstarts/pusher-with-nodejs-on-openshift)
- PubNub: (https://www.openshift.com/quickstarts/pubnub-on-openshift)

Message Queues

- Iron.io: (https://www.openshift.com/quickstarts/ironmq-on-openshift)

Communication

- Twilio - SMS/Voice: (https://github.com/jaboutboul/twilio-php-openshift-quickstart)
- SendGrid - Email: (https://www.openshift.com/quickstarts/sendgrid-on-openshift)



Another benefit is the ability for OpenShift to run a large set of languages on the backend due to the plug and play aspect of its cartridge system. Whatever your language of choice is, you just have to create your application with it. 
