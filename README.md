## Meme Magic

It's a terrible name, I know. Doesn't summarize this app at all. Here it is:
Meme Magic is a heavy handed backend boiler plate (Sockets, PSQL, Sessions, Routes, some beginnings of Auth) with some very light front end stuff set up. What little is set up on the front end is beautiful (PropTypes, Immutable.js for Redux Store, ES6, AFrame - with all of AFrames caveats built in to avoid race conditions), and the backend is fully set except your choice of login system at the moment.

I made this boiler plate able to switch between AFrame with React/Redux - or to strictly be a React/Redux boiler plate. It defaults to AFrame with React/Redux - to switch this, check out installation below.

## Motivation

I built this to be a performant, easy to deploy, ES6 God, and most importantly - boiler plate for my students at Fullstack Academy to get a good glimpse of boiler plate work and the foundation for a good app - as well as have an easier start into AFrame.

## Installation

This codebase has two criteria:

  # DB Setup

  I am sadly a WSL user (Yes, Windows, Subsystem, (for) Linux), so I can't run post-install pg-init scripts. So step 1 is make a new psql database named `meme-magic`. Thats it.
  
  If you wanted a DB named whatever you want it to be named

  # Secrets

  Make a `secrets.js` file in the root directory. It should contain:

  `export default {
    SessionKey: 'WhateverYouWant'
  };`

  # AFrame w/ React/Redux or just React/Redux

  Go to `./browser/react/containers/index.js` -> From there you will see this logic:

```
// This is React/Redux.
import AppCon from './AppContainer';

// This is AFrame w/ React/Redux.
import AFCon from './AFrameContainer';

export const AppContainer = AFCon;
```

  Just switch it to export whichever beginning plate you would like to use.

That's it. Enjoy.

## Some Known Confusion

  I have had some annoying experiences with socket leakage and Node. Until I get around to having Redis be a part of the backend to deal with enabling more than 25 sockets per Node instance - I have a mechanism set up to ensure each user (being a person) only gets 1 socket per IP. *This means that if you try to open two tabs of your project on the same machine - you get Rick Rolled away from my site.* To disable such beautiful functionality simply go to `./browser/sockets/index.js`. You will see some well commented code about a certain socket event named `KickTroll` - just change its behavior to anything else or remove it.
  
  The only other one I can remember at present is the requirement to enter `y` or `n` on intialization of the DB to decide whether to force sync the DB. This too can easily be removed in the root directory `./app.js`:

```
const syncTruth = getYesNo(chalk.cyan('Rick, do you wanna get savage on this database? (Force Sync)'));

 // If you want to disable this - change syncTruth to: 
 // const syncTruth = false : wont ever forceSync.
 // or 
 // const syncTruth = true : will always forceSync.
 
startDB(syncTruth)
  .then(() => server.on('request', myServer))
  .then(() => ioInit(server))
  .catch(err => console.error(err))
  .finally(() => server.listen(_Port, () => console.log(chalk.magenta(`Meme magic has begun on Port ${_Port}`))));
```

## Tests

Tests and deciding on the easiest Authentication to use are my current step in this project - 2/1/17

## License

Apache 2.0
