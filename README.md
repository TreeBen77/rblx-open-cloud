# rblx-open-cloud
 
Python API wrapper for [Roblox Open Cloud](https://create.roblox.com/docs/open-cloud/index).

## Quickstart

### Generating an API key and Preparing the library

1. Create an API key from the [Creator Dashboard](https://create.roblox.com/credentials). Read [Managing API Keys](https://create.roblox.com/docs/open-cloud/managing-api-keys) if you need help.
2. Copy the code in `rblx-open-cloud.py`, paste it in a new file and save it in the same directory as your project. (I'll work out how to add it to PyPi later.)
3. Add the following lines to your code and replace `api-key-from-step-1` with the key you generated in step 1. *Tip you should add your api key to an enviroment variable.*
    ```py
    import rblx_opencloud
    rblx_opencloud.api_key = "api-key-from-step-1"
    ```
    **If you want to start by accessing your game's data stores go to [Data Stores](#accessing-data-stores) otherwise, you can go to [Place Publishing](#publish-or-save-a-rbxl-file).**
> **note:** Roblox doesn't support access to ordered data stores via open cloud, yet.

### Publish or Save a `.rbxl` File
```py
import rblx_opencloud
rblx_opencloud.api_key = "api-key-from-step-1"

#create a PlacePublishing object with your universe
PlacePublishing = rblx_opencloud.PlacePublishing(universe="universe-id-here")

#opens the .rbxl file as 'rb' and saves it to the place
with open("path-to/place-file.rbxl", "rb") as file:
    version = PlacePublishing.savePlace("place-id-here", file)

#opens the .rbxl file as 'rb' and publishes it to the place
with open("path-to/place-file.rbxl", "rb") as file:
    version = PlacePublishing.publishPlace("place-id-here", file)
```

### Accessing Data Stores

If you don't know how to get the universe or place ID read [Publishing Places with API Keys](https://create.roblox.com/docs/open-cloud/publishing-places-with-api-keys#:~:text=Find%20the%20experience,is%206985028626.)
```py
import rblx_opencloud
rblx_opencloud.api_key = "api-key-from-step-1"

# create a DataStoreService object with your universe ID
DataStoreService = rblx_opencloud.DataStoreService(universe="universe-id-here")

# get your data store, scope is default to global
DataStore = DataStoreService.getDataStore("data-store-name", scope="global")

# gets the value and info (user ids, metadata, created, etc.)
value, info = DataStore.get("key-name")

# sets the value of the key and assigns the user ids list to 287113233
DataStore.set("key-name", "value", users=[287113233])

# deletes the key now.
DataStore.remove("key-name")
```

### Publishing To Message Service
If you don't know how to get the universe or place ID read [Publishing Places with API Keys](https://create.roblox.com/docs/open-cloud/publishing-places-with-api-keys#:~:text=Find%20the%20experience,is%206985028626.)
```py
import rblx_opencloud
rblx_opencloud.api_key = "api-key-from-step-1"

# create a MessagingService object with your universe ID
MessagingService = rblx_opencloud.MessagingService(3499447036)

#publish a message to the topic 'topic69420'. Roblox Studio won't recieve this message, only live game servers.
MessagingService.publish("topic69420", "message")
```
check out the wiki for documentation.
