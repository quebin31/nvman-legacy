# nvman

`nvman` is a manager for two services that solve the NVIDIA Optimus problem in laptops.
Sometimes you want to run a program with **bumblebee** regarding the performance, but
sometimes you want to run a program with **optimus-manager** regarding that you have to
log out and log in. That can be tedious and both services can be conflictive, if I want to
have both on my system I need to take care about who of those is enabled?, who is active
right now?, am I using `nvidia` or `intel` driver?, who is my default service? 


**WARNING:** This was only tested on Arch Linux.

## Dependencies 

- bumblebee
- primus
- optimus-manager (AUR)

## How to install (Arch Linux)

It's actually pretty easy

```yay -S nvman```

## Config

Config is system-wide at `/etc/nvman/config` and it only saves what's your default service

Example:

```
default = optimus
```

## Usage 

- If you want to run something with `primusrun`

	```nvman run 'your command'```

	Example:

	```nvman run glxgears``` 

	This will fail if you are currently using `nvidia` with `optimus`

	**More info:** `man primusrun` 

- If you want to completely use `nvidia` (This will log out you instantly)
	
	```nvman switch nvidia```
	
	Or if you want to go back to `intel` 
	
	```nvman switch intel```

	Or let `optimus-manager` toggle it for you

	```nvman switch auto```

	**More info:** [optimus-manager](https://github.com/Askannz/optimus-manager)

- Set the default service (it will enabled)

	```nvman default (optimus|bumblebee)```

- If your default service is `optimus`, set the startup mode for it 

	```nvman startup (intel|nvidia|nvidia_once)```

	**More info:** [optimus-manager](https://github.com/Askannz/optimus-manager)

- Check the current status of your NVIDIA Optimus setup

	```nvman status```

	Example output:

	```none
	Optimus: active (enabled)
	Bumblebee: inactive (disabled)
	Default service: optimus
	Default startup for optimus is intel
	Currently using nvidia with optimus
	```

## Advantages 

- Setting a default service will automatically disable the other one and save your preferences.
- Using `nvman run` will start the `bumblebee` service (if it wasn't already active) 
and stop `optimus` 
- Using `nvman switch` will start the `optimus` service (if it wasn't already active)
and stop `bumblebee`
- If you enable `nvman.service`, it will check at boot time if `optimus` and `bumblebee` are both enabled or disabled, if that happens it will enable only your default service (in order to avoid conflicts)
