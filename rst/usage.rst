.. _usage:

Usage Guide
===========
This guide will detail some best practices and suggestions to consider when developing with the PUBG API.

App Structure
-------------
An application using the API will typically have the following components:

**A client-side app**
    This is the user facing part of the application. It takes in user input, makes a request to the backend, and displays the results for the user. This could be represented as a standalone website, Discord bot, mobile app, or anything else you can think up.

**A backend server**
    This is the core logic of the application. It receives requests from the client-side app, makes appropriate requests to the API, processes the data received, stores it in the database, and returns it to the client-side app.

- **A database structure**
    This is where the aggregated data is stored. Depending on what your application does, this could be player records, match history, leaderboard standings, or anything else it needs to hold on to.

**A caching layer**
    This component sits between the backend server and the API. It speeds up user requests and reduces the number of calls to the API by storing API responses in memory. We will get more into the details of how this works in the `Caching Overview`_ and `Caching Implementation`_ sections.

**The API**
    Added for visualization in the stack, this is the PUBG API.



Intended data use
-----------------
The data provided by the PUBG API can be used in many ways to create a variety of applications. It is important to understand the intended uses of this data, and how the data and endpoint structure reflect that vision.

The primary API endpoints (players and matches) are structured to favor specific searches, and not to provide access to all data. This is why the API flow starts with searching for specific players. In general, applications should try to stick to an opt-in flow, as opposed to trying to search for all players. Here are some examples of how this flow could fit into some of the expected use cases:

- Stat sites & bots - A user must enter their player name to see their stats and history, meaning that the application only needs to query the API when that happens
- Leaderboards & coaching services - Users must register on the site, meaning that the application only has to query for known players

This being said, some applications may still need to analyze large amounts of random data. This can be done by requesting sample data, which is a randomized statistical sample that can be used to infer and understand global changes. This data can be acquired from the samples endpoint.



.. _Caching Overview:

Caching Overview
----------------
Generally speaking, applications should try to avoid querying for the same data twice whenever possible. This is where caching comes into play. When the backend makes a request to the API, the results should be cached so that they can be reused for a set period of time. 

For example, lets say that your application takes a player's IGN as input and displays their stats and match history. The first time the player is looked up by the service, the application will have to query the API to get their data. The caching layer then holds onto those API responses for a set amount of time, lets say 30 minutes. If the player is looked up again within that window, the results will be returned from memory without needing to call the API. After that window has passed the cached data will be removed. The next time that player is looked up the cycle will repeat (query API --> store in cache --> remove after 30 min).

There may also be an opportunity for caching results from the backend server depending on how your application works. This can help cut down on requests to your database or other storage structure.



.. _Caching Implementation:

Caching Implementation
----------------------
In this section we will cover how to cache API responses at a high level. Please note that the code examples shown below are in GO, and do not include error handling.

To start, let's take a look at an example function that gets a player object, which we will assume is a structure containing relevant player data for our application needs:

.. code-block:: go

    func getPlayer(playerName string) playerObject {
        apiResponse := makePlayerNameRequest(playerName) //query the API for the given player name

        if apiResponse != nil {
            //we found the player in the API
            player := processPlayer(apiResponse) //process the API response into a player object
            return player
        }
    }

This function will make a request to the API each time it is called for a specific player. This can be very inefficient considering that player records in the API are not updated frequently (at minimum, the time of a single match plus a little bit for processing time). To improve this, we can surround the existing functionality with a check for the player in the cache. In addition, we also now need to remember to store the player object in the cache when we do get it from the API. It will look something like this:

.. code-block:: go

    func getPlayer(playerName string) playerObject {
        player := getPlayerFromCache(playerName) //try to get the player object from the cache
        if player != nil {
            return player
        }

        //we couldn't find the player object in the cache
        apiResponse:= makePlayerNameRequest(playerName) //query the API for the given player name

        if apiResponse != nil {
            //we found the player in the API
            player := processPlayer(apiResponse) //process the API response into a player object

            //store the player in the cache for next time
            //this function takes in the player object to store, and an integer representing how long the object should remain in the cache
            storePlayerInCache(player, 30)

            return player
        }

        return nil
    }



Caching Software
----------------
Here are some examples of caching software:

- `Memcached <https://memcached.org/>`_ - A fairly easy to use caching software with wrappers in many programming languages.
- `Redis <https://redis.io/>`_ - A more complex caching software offering more flexibility and features
