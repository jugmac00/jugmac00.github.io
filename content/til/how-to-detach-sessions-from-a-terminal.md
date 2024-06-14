---
title: "How to Detach Sessions From a Terminal"
date: 2024-06-13T20:21:24+02:00
tags:
- linux
- terminal
- multiplexer
- tmux
- screen
- byobu
---

When we do production deployments at my team at Canonical, we log into a
bastion server and execute a long running command from there.

Long running as of 30 minutes. The script goes through all our servers and
deploys the latest changes.

Needless to say that it would not be optimal when e.g. the connection dies
during the deployment, as this would stop the deployment right in the middle.

## Hello terminal multiplexer

Most engineers probably heard of tmux and screen before. These tools allow
detaching sessions from the terminal, so even when your connection dies,
the session continues to run in the background. Sounds great, right?

I think I used these before on some rare occasions, but certainly not enough to
feel comfortable using them.

My colleague [Guruprasad](https://www.lguruprasad.in/) pointed me to another
tool - [Byobu](https://www.byobu.org/) - which seemed to be another terminal
multiplexer, but actually it is just a wrapper script, and uses tmux or screen
in the background. The difference? Byobu is super easy to get started with.

## Byobu in five easy steps

* start a session

```
byobu
```

* leave a session

press ```F6```

* activate scrolling mode

press ```F7```

* scroll

use arrow keys or ```PageUp``` and ```PageDown```

* end a session

```
exit
```

That's all!

## Further information

* Official website: https://www.byobu.org/
* Open builtin help: ```Shift + F1```
* [Learn Byobu while listening to Mozart](https://www.youtube.com/watch?v=NawuGmcvKus)




