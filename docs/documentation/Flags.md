&nbsp;&nbsp;&nbsp;&nbsp;:octicons-info-16:&nbsp;&nbsp;*For the flag glossary, [click here](Glossary).*

### **Description**

Flags are boolean (`ON`/`OFF`) variables that help the game keep track of progress.<br>
There are 255 flags in the game, each with different saving properties that can be divided into one of three groups: Savable Flags, Room Flags, and Map Flags.

The status of these flags can be checked with JMP Tables, Events, and ASM.<br>

!!! info "Types of Flags"

	=== "Savable Flags<br>(1-84)"
		Once these flags are turned `ON`, they will stay `ON`. The state of these flags can be saved to the memory card.
		Resetting without saving is the only way these flags reset back to `OFF`.

		- [x] Can save ON/OFF status to memory card.
		- [x] If ON, flag stays ON after leaving current map.
		- [x] If ON, flag stays ON after leaving current room.

	=== "Room Flags<br>(85-169)"
		Once these flags are turned `ON`, they'll only be active for the current <u>room</u> Luigi is in. If Luigi exits the room, these flags will reset back to `OFF`.

		- [ ] Can save ON/OFF status to memory card.
		- [ ] If ON, flag stays ON after leaving current map.
		- [ ] If ON, flag stays ON after leaving current room.

	=== "Map Flags<br>(170-255)"
		Once these flags are turned `ON`, they'll only be active for the current <u>map</u> Luigi is in. If Luigi warps to a different map, these flags will reset back to `OFF`.

		- [ ] Can save ON/OFF status to memory card.
		- [ ] If ON, flag stays ON after leaving current map.
		- [x] If ON, flag stays ON after leaving current room.

### **Usage in Events**
Flags can be checked, turned `ON`, and turned `OFF` in events.

::spantable::

| Script Tag | Description                                                                                                                            |
| :--------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| CHECKFLAG  | Checks the state of the flag (#) specified, then jumps to the first case if the flag is `ON` and the second case if the flag is `OFF`. |
| EVENTWAIT  | Turns `ON` the flag (#) specified and halts the script whilst waiting for the flag to be turned `OFF`, usually done so through ASM.    |
| FLAGOFF    | Turns `OFF` the flag (#) specified.                                                                                                    |
| FLAGON     | Turns `ON` the flag (#) specified.                                                                                                     |

::end-spantable::

#### **Special Usage in Events**

### **Usage in JMP**
Flags can be turned `ON`, used as spawn conditions, and as despawn conditions in JMP files.

::spantable::

| Field Name              | JMP File(s)                                                                                                                                       | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <br>appear_flag<br><br> | characterinfo, enemyinfo, furnitureinfo, generatorinfo, keyinfo, objinfo, observerinfo, teidencharacterinfo, teidenenemyinfo, teidenkeyinfo @span | This flag will allow/disallow the desired actor/object to spawn. Note that this is calculated upon room load, so turning a flag `ON` in a room will not make this actor/object spawn/despawn until room reload.<br><br>A good trick is to use the `<TURNON>` script tag in an event, which turns off the blackout, refreshing the listed JMP files except `furnitureinfo` and `objinfo`. @span |
| disappear_flag          |                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                |
| cond_type               | characterinfo, enemyinfo, keyinfo, teidencharacterinfo, teidenenemyinfo, teidenkeyinfo                                                            | [Condition Types](#condition-types)                                                                                                                                                                                                                                                                                                                                                            |
| do_type                 | observerinfo                                                                                                                                      | [Do Types](#do-types)                                                                                                                                                                                                                                                                                                                                                                          |
| arg0                    | furnitureinfo, observerinfo                                                                                                                       | [Move Types](#move-types), [Condition Types](#condition-types)                                                                                                                                                                                                                                                                                                                                 |
| arg1                    | furnitureinfo @span                                                                                                                               | [Move Types](#move-types) @span                                                                                                                                                                                                                                                                                                                                                                |
| arg2                    |                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                |
::end-spantable::

#### **Condition Types**
Some observer *cond_type* can check flag status.

::spantable::

| Condition<br>Type # | Class Name       | observerinfo<br>Fields Used | Description                                        |
| ------------------- | ---------------- | --------------------------- | -------------------------------------------------- |
| 18                  | CondEventFlagOn  | cond_arg0                   | Checks if the flag listed in *cond_arg0* is `ON`.  |
| 19                  | CondEventFlagOff | cond_arg0                   | Checks if the flag listed in *cond_arg0* is `OFF`. |

::end-spantable::

##### **Special Condition Types**
These condition types check flags in a more specific manner.

::spantable::

| Condition<br>Type # | Class Name          | observerinfo<br>Fields Used | Description                                                          |
| ------------------- | ------------------- | --------------------------- | -------------------------------------------------------------------- |
| 4                   | SaEnCheckTime       | arg0                        | If the flag given in arg0 is `ON`, the GBH time will not be checked. |
| 11                  | CondStartFromScript | *N/A*                       | Activates only when flag 91 is turned `ON`.                          |

::end-spantable::

#### **Do Types**
Some observer *do_type* can turn a flag `ON`.

::spantable::

| Do Type # | Class Name       | observerinfo<br>Fields Used | Class Name                                                                                   |
| --------- | ---------------- | --------------------------- | -------------------------------------------------------------------------------------------- |
| 3         | SaEnTelephone    | arg0, arg1                  | If the flag in arg1 is turned `ON`, then turned `OFF`, the flag in arg0 will be turned `ON`. |
| 7         | EnSetEventFlagOn | arg0                        | Turns the flag listed in arg0 `ON`.                                                          |
::end-spantable::

#### **Move Types**

Some furniture *move* types can turn a flag `ON`.

::spantable::

| Move<br>Type # | Behavior              | furnitureinfo<br>Fields Used | Description                                                                          |
| -------------- | --------------------- | ---------------------------- | ------------------------------------------------------------------------------------ |
| 16             | Books                 | arg0 @span                   | When Luigi interacts with the furniture, the flag in arg0 will be turned `ON`. @span |
| 33             | Button                |                              |                                                                                      |
| 43             | Angel Statue          |                              |                                                                                      |
| 38             | Furniture with a Door | arg0, arg1                   | If arg0 = 1, the furniture will turn the flag listed in arg1 `ON` when opened.       |

::end-spantable::

##### **Special Move Types**
These move types interact with flags in a more specific manner.

::spantable::

| Move<br>Type # | Behavior               | furnitureinfo<br>Fields Used | Description                                                                                                                                                                                                                                                               |
| -------------- | ---------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 5              | Rocking Chair          | *N/A*                        | It will turn flag 169 `ON` at its max speed (when vacuumed) if Chauncey is present.                                                                                                                                                                                       |
| 6              | Musical Instrument     | *N/A*                        | Only when in room 23 when Melody is present, activating all furniture with this type will turn flag 88 `ON`. If flag 90 is turned `ON`, the music from these furniture will stop playing.                                                                                 |
| 8              | Helicoptor Mobile      | *N/A*                        | It will turn flag 88 `ON` when spun enough times with the vacuum.                                                                                                                                                                                                         |
| 9              | The Observatory        | arg2 @span                   | If arg2 is set to 1, then the furniture will gradually fade in once flag 50 is turned `ON`. If arg2 is set to 0, then the furniture will gradually fade out once flag 50 is turned `ON`. @span                                                                            |
| 10             | Observatory Telescope  |                              |                                                                                                                                                                                                                                                                           |
| 13             | Observatory Chandelier |                              |                                                                                                                                                                                                                                                                           |
| 11             | Crystal Ball           | *N/A*                        | It will turn flag 88 `ON` when shined on long enough with the flashlight.                                                                                                                                                                                                 |
| 12             | Storage Room Wall      | *N/A*                        | It only moves once flag 41 is turned `ON`.                                                                                                                                                                                                                                |
| 14             | Parlor Painting        | *N/A*                        | While flag 94 is `ON`, the furniture will shake.                                                                                                                                                                                                                          |
| 20             | Foyer Chandelier       | *N/A*                        | While flag 1 is `ON`, the furniture is allowed to crash down and hurt Luigi during Area 1.                                                                                                                                                                                |
| 24             | Alternate Observatory  | *N/A*                        | It will turn flag 50 `ON` when shaken.                                                                                                                                                                                                                                    |
| 25             | Bogmire's Tomb         | *N/A*                        | Allows the BMD effect *boseki* to be attached to the furniture when flag 74 is `ON`.                                                                                                                                                                                      |
| 31             | Storage Room Boo Hatch | arg0                         | It only moves when the flag in arg0 is `ON`.                                                                                                                                                                                                                              |
| 36             | Projector              | *N/A*                        | It will turn flag 114 `ON` when shaken.                                                                                                                                                                                                                                   |
| 39             | Van Gore Painting      | arg0                         | The camera and particle effects will only occur when the flag in arg0 is set to `ON`. When flag 55 is turned `ON` by capturing Van Gore, the effects of the furniture will turn off. If arg0 is set to 55, the furniture will spawn whatever item is set in *item_table*. |
| 40             | Pipe Room Handle       | *N/A*                        | It only moves when flag 63 is turned `ON`.                                                                                                                                                                                                                                |
| 41             | Breaker Room Switch    | *N/A*                        | It only moves when flag 115 is turned `ON`.                                                                                                                                                                                                                               |
::end-spantable::

### **Availabile Flags**
See the [flag glossary](Glossary).
