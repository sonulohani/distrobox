<!-- markdownlint-disable MD010 MD036 -->
# NAME

	distrobox-upgrade

# DESCRIPTION

distrobox-upgrade will enter the specified list of containers and will perform
an upgrade using the container's package manager.

# SYNOPSIS

**distrobox upgrade**

	--help/-h:		show this message
	--all/-a:		perform for all distroboxes
	--verbose/-v:		show more verbosity
	--version/-V:		show version

# EXAMPLES

Upgrade all distroboxes

	distrobox-upgrade --all

Upgrade a specific distrobox

	distrobox-upgrade alpine-linux 

Upgrade a list of distroboxes

	distrobox-upgrade alpine-linux ubuntu22 my-distrobox123

**Automatically update all distro**

You can create a systemd service to perform distrobox-upgrade automatically,
this example shows how to run it daily:

~/.config/systemd/user/distrobox-upgrade.service

	[Unit]
	Description=distrobox-upgrade Automatic Update

	[Service]
	Type=simple
	ExecStart=distrobox-upgrade --all
	StandardOutput=null

~/.config/systemd/user/distrobox-upgrade.timer

	[Unit]
	Description=distrobox-upgrade Automatic Update Trigger

	[Timer]
	OnBootSec=1h
	OnUnitInactiveSec=1d

	[Install]
	WantedBy=timers.target

Then simply do a `systemctl --user daemon reload && systemctl --user enable --now distrobox-upgrade.timer`
