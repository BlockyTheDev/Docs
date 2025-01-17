**Table of context**
* [Shortcuts](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#shortcuts)
* [Checks](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#checks)
* [Specific](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#specific)
* [Commands](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#commands)
* [Auxiliary commands](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#auxiliary-commands)
* [Miscellaneous and parent permissions](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#miscellaneous-and-parent-permissions)
* [Configure permission caching behavior](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Permissions.md#configure-permission-caching-behavior)

# Shortcuts
`nocheatplus.shortcut.info` Gives permissions to  
`nocheatplus.shortcut.monitor` Gives permissions for  
`nocheatplus.shortcut.safeadmin` Gives permissions to  
`nocheatplus.shortcut.bypass` Gives permissions to bypass all checks.  

# Checks
`nocheatplus.checks` Exempts from all checks  
`nocheatplus.checks.<Check category here>` Exempts from all checks of a given check category.  
`nocheatplus.checks.<Check category here>.<Check name here>` Exempts group of this check. (Example: nocheatplus.checks.moving.creativefly will exempt from CreativeFly).

## Specific
`nocheatplus.bypass.denylogin` Exempts from login denial.  
`nocheatplus.checks.blockplace.boatsanywhere` Allows to place boats on the ground (not just in water).  
`nocheatplus.checks.blockbreak.break.liquid` Allows to break water/lava through cheats.
<br>`nocheatplus.checks.moving.survivalfly.speeding` Extra speed permission for [SurvivalFly](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Checks/%5BMoving%5D-Survivalfly.md).</br>
`nocheatplus.checks.moving.survivalfly.sprinting` Will exempt players from getting checked for backwards and blindness sprinting.
`nocheatplus.checks.moving.survivalfly.step` Will exempt players from SurvivalFly's step cheat modules.</br>
`nocheatplus.checks.moving.survivalfly.sneaking` Exempt players from the horizontal limits for sneaking.</br>
`nocheatplus.checks.moving.survivalfly.blocking` Exempt players from the horizontal limits for blocking/shielding.
`nocheatplus.checks.moving.survivalfly.waterwalk` Will exempt players from getting checked by SurvivalFly's main waterwalk checks.

# Commands
`nocheatplus.command.commands` Can view all NC+ commands with _/ncp commands_  
`nocheatplus.command.exempt` Can exempt players from checks with _/ncp exempt_  
`nocheatplus.command.exemptions` Can list all check exemptions of a player with _/ncp exemptions_  
`nocheatplus.command.info` Can view check violations of a player with _/ncp info_  
`nocheatplus.command.inspect` Can retrieve player status data with _/ncp inspect_  
`nocheatplus.command.lag` Can view server lag spikes with _/ncp lag_  
`nocheatplus.command.log` Can access internal debug data with _/ncp log_
<br>`nocheatplus.command.notify` Can toggle on/off in-game cheat notifications (includes permission `nocheatplus.notify`) for _/ncp notify_ command)</br>
`nocheatplus.notify` Can view NC+ in-game notifications (but can't toggle them on/off without the permission above)
`nocheatplus.command.reload` Can reload NC+ to re-read configurations and permissions with _/ncp reload_  
`nocheatplus.command.removeplayer` Can remove a players violation history with _/ncp removeplayer_  
`nocheatplus.command.unexempt` Can unexempt a player from checks with _/ncp unexempt_  
`nocheatplus.command.version` Can view the version information with _/ncp version_  

## Auxiliary commands
`nocheatplus.command.allowlogin` Can remove temporary kicked players with _/ncp allowlogin_  
`nocheatplus.command.ban` Can ban players with _/ncp ban_  
`nocheatplus.command.delay` Can delay command execution with _/ncp delay_  
`nocheatplus.command.denylogin` Can temporary kick players with _/ncp denylogin_  
`nocheatplus.command.kick` Can kick players with _/ncp kick_  
`nocheatplus.command.kicklist` Can view all players that have been temp-kicked with _/ncp kicklist_  
`nocheatplus.command.tell` Can send private messages to players using _/ncp tell_  

# Miscellaneous and parent permissions

`nocheatplus.admin` Gives access to all [NoCheatPlus commands](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Commands.md) including Auxiliary ones  
`nocheatplus.notify` Will receive hack notifications over in-game chat

Commands for which the permission got set by the protection features (hide plugins), might have altered default permissions or NoCheatPlus may have set a filter permission 'nocheatplus.filter.command.COMMAND_NAME', for the case the command was allowed to be run by everyone.

**Notes**
* By default NoCheatPlus assigns all permissions and gives full rights to players that have been `/op-ed` on your server. If you don't want to give OPs full access to all NoCheatPlus features then take a look in the configuration of your permissions plugin (Example with PermissionsEx: allowOps: false).

**Related**
* [Checks](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Checks/Checks.md)
* [Commands](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Settings/Commands.md)
* [Debugging](https://github.com/Updated-NoCheatPlus/Docs/blob/master/Development/Debugging.md)

# Configure permission caching behavior
Since NoCheatPlus 3.16.1-SNAPSHOT (since build 1040) / 3.17.0-RC, permission caching has been introduced. This allows for configuration of how to check for permissions, in case permission checks turn out to consume too much performance, or in case you want to override the behavior for other reasons.

You can set a default policy and define further rules for mapping permissions to policies for individual permissions, based on wildcards, or based on regular expressions.

Policy definition:
* Fetching policy[, flag1 [,flag2]]
* Separate any parts by ' ' or ',' or ':'.
* Flags are preceded by the state '+' for true and '-' for false. Default flag states can be omitted, such as `+world` or `+offline`.
* Flags apply for invalidation, regardless of the fetching policy.

| Fetching policies | Meaning/usage |
| ----------------- | ------------- |
| ALWAYS | Always check. |
| ONCE  | Once until invalidation. |
| INTERVAL:_(seconds)_ | Only check every _(seconds)_ seconds. |
| TRUE | Always assume permission to be set to true. |
| FALSE | Always assume permission to be set to false. |

| Policy flags| Meaning/usage |
| ----------- | ------------- |
| +offline | Invalidate permissions once the player is offline (default). Strictly this also invalidates with logging on. |
| -offline | No invalidation with leaving the server, unless +world is set (!). |
| +world | Invalidate with world changes and leaving the server (default).|
| -world | No world based invalidation. Behavior with leaving the server depends on the `offline` flag now. |

Rule definition:
* Matching rule separated by ' :: ' from a policy definition.

| Matching rule | Meaning/usage |
| ------------- | ------------- |
| _(directly the permission, excluding the variants given below.)_ | Match only that permission |
| startswith:_(...)_ _or_ _(...)_* | All permissions that start with the given part. |
| endswith:_(...)_ _or_ *_(...)_ | All permissions that end with the given part. |
| contains:_(...)_ _or_ \*_(...)_\* | All permissions that contain the given part. |
| regex:_(regular expression pattern)_ | All permissions matching the regular expression pattern (standard java String.matches). |
(Constructions with * _(...)_ * _(...)_ * don't work, use regular expressions instead.)

## Default policy
* Configuration path: permissions.policy.default
* Value: string
* Content: policy definition
* Examples: 
    * `INTERVAL:10, -offline, -world` for checking every 10 seconds, ignoring world changing and leaving the server.
    * `ONCE` for checking once only, still invalidate with changing the world and with logging on/off.

## Rules
* Configuration path: permissions.policy.rules
* Value: String list.
* Content: matching rule separated by ' :: ' from a policy definition.
* The first matching rule is applies, testing in the order in which they're defined.
* Examples:
    * See default configuration...
    * `nocheatplus.checks.survivalfly.* :: FALSE, -offline, -world` Never check the sub permissions of survivalfly, assume set to false always.
    * `startswith:nocheatplus.checks.survivalfly. :: FALSE, -offline, -world` Same as above.
    * `nocheatplus.checks.survivalfly* :: INTERVAL:10` Check the survivalfly permission and sub permission only every 10 seconds (invalidate with logging on/off and with world changing).
