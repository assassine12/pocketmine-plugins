<img src="https://raw.githubusercontent.com/alejandroliu/bad-plugins/master/Media/rss.png" style="width:64px;height:64px" width="64" height="64"/>

# LiveSigns

* Summary: Display updating messages on signs
* Dependency Plugins: N/A
* PocketMine-MP version: 1.5 - API 1.12.0
* DependencyPlugins: -
* OptionalPlugins: N/A
* Categories: Informational
* Plugin Access: Tiles, Internet Services, Commands
* WebSite: [github](https://github.com/alejandroliu/bad-plugins/tree/master/RssSigns)

## Overview


LiveSings is a plugin to display texts in signs from a number of
sources and can change automatically as the sources change.

Currently available sources:

* configuration file
* text file
* web url
* RSS feed
* Twitter feed

A sample configuration files are provided to get you started.  Basic
usage is that you create a LiveSign source, and assign it an id.  Then
in the game you place a sign with that id, and it will start
displaying it.


Sign Format:

* **[livesign]**
* _id_
* _line:step_

The entry _line:step_ is optional and is used to have multi-sign
messages.

## Documentation

Use the **/livesign** command to access the plugin functionality.  The following sub-commands are available:

* **cfg** _[id]_
   * show the configured sources
* **show** _[id]_
   * show the retrieved texts
* **set** _<id>_ _<type>_ _<content>_
   * create a new source with _id_.  See source types for the _type_.
* **rm** _<id>_
   * remove a livesign source
* **update** _<id>_
   * retrieve again the text for the specified source.
* **reload** _<id>_
   * reload signs configuration.
* **status**
   * show status of async task
* **announce** _<id>_
   * broadcast the livesign on the chat

### LiveSign sources

* text
  * This is text embedded in the signs.yml file.  Can be
     a single line, or if multiple lines are needed, then
    you can provide them as a list.
* file
  * Points to a file in the plugin directory.
* url
  * points to a URL that will be fetched.
* rss
  * points to an URL to an RSS feed.  The content
     must contain the URL.  You can optionally provide
     additional settings to select an item from a feed or
     the atom to display
* twitter
  * points to a twitter feed.  You can optional provide
     a number which picks the update.

### Enabling Twitter feeds

First you need to create a twitter app.  To do that go to
[How to register a Twitter App](http://iag.me/socialmedia/how-to-create-a-twitter-app-in-8-easy-steps/)
and configure your twitter details in config.yml:

```
[CODE]
'oauth_access_token' => "YOUR_OAUTH_ACCESS_TOKEN",
'oauth_access_token_secret' => "YOUR_OAUTH_ACCESS_TOKEN_SECRET",
'consumer_key' => "YOUR_CONSUMER_KEY",
'consumer_secret' => "YOUR_CONSUMER_SECRET"
[/CODE]
```

### Multi sign's messages

Since the space in a sign is quite limited, sometimes is necessary to
span a message accross multiple signs.  This is accomplished using the
_line:step_ setting that is on the third line of a sign.  The way it
works is that the LiveSign text is split into lines.  The first number
in _line:step_ is the starting line number (the first line is zero).
Then, for the second line in the sign, we would add _step_ and pick
the corresponding line of the message.  So if you want to make a
message made of 2 signs accross, you would have:

| 0:2 | 1:2 |

Whereas if you wanted to have a message of 3 signs accross, 2 signs
up you would use:

| 0:3 | 1:3 | 2:3 |
| 12:3 | 13:3 | 14:3 |


### Additional Libraries

* RSS support: [lastRSS](http://lastrss.webdot.cz/)
* Twitter Support: [Twitter-API-PHP](http://github.com/j7mbo/twitter-api-php)

### Configuration

Configuration is throug the `config.yml` file.
The following sections are defined:

#### main

*  settings: tunnable parameters
	*  tile-updates: How often to update signs in game from cache (in-ticks)
	*  cache-signs: How long to cache sign data (seconds)
	*  expire-cache: How often to expire caches (ticks)
	*  path: file path for the file fetcher
	*  twitter: Used by the twitter feed fetcher
*  signs: trigger text


### Permission Nodes

* livesigns.cmd : Main livesign command
  (Defaults to Op)
* livesings.cmd.addrm : Update livesign
  (Defaults to Op)
* livesings.cmd.info : Show status of livesigns
* livesings.cmd.update : Refresh livesigns
  (Defaults to Op)
* livesings.cmd.broadcast : Broadcast livesigns in chat
  (Defaults to Op)


# Changes

* 1.0.0 : First submission

# Copyright

    LiveSigns
    Copyright (C) 2015 Alejandro Liu
    All Rights Reserved.

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
