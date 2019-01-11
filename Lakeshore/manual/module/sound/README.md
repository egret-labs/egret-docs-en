![](564af1ef17212.png)

The sound component is used to add sound effects to games.

### Unique properties
![](564af1eecf6a9.png)
- File Path: specify the location of sound files.
- Cycle times: set the cycle times of sound. The default value is 1. It means infinite cycle if you set the value as 0.
- Volume: set the volume of the sound. The default value is 1, means 100%

*Note: the sound component does not support basics properties except the “name”. It doesn’t support collisions, and will not produce visible instances in the running scene of game after adding.

------------


### Sound conditions
Sound components only support its unique conditions and do not support general conditions.

![](564af1eee846a.png)
#### When muted
When it's in muted condition.【continuous trigger】
This condition has no property settings window.
#### When sound is played
When any sound is playing.【continuous trigger】
This condition has no property settings window.
#### When a specified sound is played
When a specified sound is played.【continuous trigger】
Set the specified sound location in the file address input box.
![](564af1ef06d2f.png)
#### When the sound is finished
When we finished the sound play. 【one-time trigger】
This condition has no property settings window.

------------


### Sound Actions
Sound components only support its unique actions and do not support general actions.

![](564af1ee25028.png)
#### Play
Play the specified sound.
- File path: specify the path of file you want to play.
- Cycles: set the cycle times, the default value is 0, means infinite cycle.
- Volume: set the volume level. The default value is 1, mens 100%.

![](564af1ee4db9a.png)
#### Stop the specified sound
Stop the playback of the specified sound.
![](564af1ee7497d.png)
#### Stop all sounds
stop playing all sounds.
This action has no property settings window.
#### Cycle
Set whether the specified sound is cycle played or not.
![](564af1ee84f3e.png)
#### Master Volume
Set overall volume.
![](564af1eeb692a.png)
#### Specify sound volume.
Set the volume of specified sound.
![](564af1eea5afe.png)
#### Mute
Set the specified sound as mute.
![](564af1ee66b4f.png)
#### Pause
Pause the specified sound.
![](564af1ee98d40.png)   


