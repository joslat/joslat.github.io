---
layout: post
title: GraphQL, the new API standard
subtitle: I discovered it by chance by the end of last year and now I am convinced..
bigimg: /img/path.jpg
tags:
  - API
  - Azure
published: true
date: '2020-02-29'
---

**It all began last year..**
## I attended a user group meeting and my eyes opened to a new path ahead.. 
Yes sounds too much prose but I was blind and not looking far away than what I already knew..
It was by the end of October, on the local user group that I have been running forever a bit after I arrived  at Zurich.. I was not supposed to host the event as the team has grown in pretty talented people, check here the outstaning team behind the [.NET Zurich Developers User Group](https://www.dotnet-zurich.ch/).
But one of my UG colleagues was ill and could not go and asked me to. It was a good decision to accept.
Or come to our next talk, next Tuesday: [Hint: It's about GraphQL & Blazor](https://www.meetup.com/dotnet-zurich/events/267725200/)

## I learned about GraphQL
And also got some friends, which is also cool. I learned that what I thought was right was not. REST was not the culmination of the web API Backend "deified" pillar for all data to be served.. Even I know it had problems, I sort of had engraved that it was the "way to go".
Not anymore.

**I met Michael.. And Rafi..** They showcased GraphQL standard on that evening and explained extensively how the differences. And more important why it was created.. at 2012 it was created by Facebook in order to solve the issues that they were having with REST:
- Multiple endpoints are needed, one for each piece of information.
- Overfetching of the data (sending-receiving more data than needed)
- Underfetching (sending less data than needed)
- N+1 problem (one call will trigger several other requests for data - and to wait for them due to latency). 

With GraphQL there is one endpoint, no over or under fetching, and the N+1 problem is solved in a big way. We can ask from a Client of the API what we want and we get exactly that, in a single call.

If you are curious on more details, you can read [on the official documentation here](https://www.howtographql.com/basics/1-graphql-is-the-better-rest/) or you can check [the Talk from last october](https://www.youtube.com/watch?v=2QLhcqFYRpg)- or see it here:
[![October .NET UG Zurich](http://img.youtube.com/vi/2QLhcqFYRpg/0.jpg)](http://www.youtube.com/watch?v=2QLhcqFYRpg "October .NET UG Zurich")

## But, let's build something..
I am a firm believer that you learn from doing and once you have a graps the best path of action is start with a simple step. So let's do that.
I have been playing along with the implementation provided by the HotChocolate library and really like it a lot. Might put some comparisons in next posts with other libraries.

**Let's build the Star Wars API..** It's a common practice to put this example and we get a ready-made template from the creators of the HotChocolate GraphQL API Implementation. It is created using a Pure Code-First approach which I particularly like, as it provides more control and clarity.

We will Install the template with the following command:

`dotnet new -i HotChocolate.Templates.StarWars`

then we will crate the folder for the project and create the project.
```
mkdir starwars
cd starwars
dotnet new starwars
cd starwars
```

And we can run the project:

`dotnet run --urls="http://localhost:5000"`

Now, our API is hosted http://localhost:5000/graphql/. We can access our just baked GraphQL API with [a plain browser](http://localhost:5000/graphql/playground/)

We can query for the some characters where we want name and height:
```
query{
  characters{
    nodes{
      name
      height
    }
  }
}
```
Click on execute and we should be seeing the same results: 
Inline-style: 
![Playground](https://github.com/joslat/joslat.github.io/blob/master/img/playground.PNG?raw=true "Playground")

You can also click on the "Schema" tab and explore the data. The documentation is automatically generated, Type safe too.


**Some fine tuning**
If you are lazy like me, you do not want to type the --urls parameter every.single.time... right? (and I always forget one of the "-" somehow.. LOL)

We can open the project, go to Program.cs and we add the UseUrls fucntion right after the UseStartup. 
`.UseUrls("http://localhost:5000/")`

It should look like this:
```
        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                    webBuilder.UseStartup<Startup>()
                    .UseUrls("http://localhost:5000/")
                    );
```



## Conclusion & Takeaways
This time it was truly eye opener, so much has went through and in two days Michael Staib, one of the speakers of the previous event and me will be speaking again but adding Blazor to the equation. If we manage to get the demo "livecoding" down in time (that's on me so to say...) It's going to be real cool session so if you are around, come and join! 

**Cool Event here**: [Hot & Fast: Implementing GraphQL backend & Blazor frontend with HotChocolate!](https://www.meetup.com/dotnet-zurich/events/267725200/)

So, to conclude take this with you:
- Be open. I believe we have to be open to new ideas, listen to people and specially to people that are willing to share. It's fun and you can end up learning something! 
- Listen to your peers, be open to discussions. This is part of the learning process where you solidify what you just learned. Question everything, challenge your peers, yourself and even, the speaker.
- Go to user group meetings: you can learn (you probably will), you will have fun and if you talk to people you might end making friends.
- Ah yes, GraphQL is cool and do check out HotChocolate ;)

**Update: we have video..**
I created a video for the API creation process so feel free to watch it and follow it along. 

[![Follow-along video for the GraphQL API demo](http://img.youtube.com/vi/r1GPXDV6ets/0.jpg)](http://www.youtube.com/watch?v=r1GPXDV6ets "Follow-along video for the GraphQL API demo")

Disclaimer: It's my first time doing this so do not expect great quality... I'd say it's close to "acceptable"

**Till next time ;)**
In the next post we will, together, build a blazor client and consume the API we just created. Sounds cool? Feel free to follow me!


happy coding!  
Jose
