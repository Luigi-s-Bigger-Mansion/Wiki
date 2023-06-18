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

### **Flags in Events**
Flags can be checked, turned `ON`, and turned `OFF` in events.

::spantable::

| Script Tag | Description                                                                                                                            |
| :--------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| CHECKFLAG  | Checks the state of the flag (#) specified, then jumps to the first case if the flag is `ON` and the second case if the flag is `OFF`. |
| EVENTWAIT  | Turns `ON` the flag (#) specified and halts the script whilst waiting for the flag to be turned `OFF`, usually done so through ASM.    |
| FLAGOFF    | Turns `OFF` the flag (#) specified.                                                                                                    |
| FLAGON     | Turns `ON` the flag (#) specified.                                                                                                     |

::end-spantable::

### **Flags in JMP**
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

#### Condition Types
Some observer *cond_type* can check flag status.

::spantable::

| Condition<br>Type # | Class Name       | observerinfo<br>Field | Description                                        |
| ------------------- | ---------------- | --------------------- | -------------------------------------------------- |
| 18                  | CondEventFlagOn  | *cond_arg0*           | Checks if the flag listed in *cond_arg0* is `ON`.  |
| 19                  | CondEventFlagOff | *cond_arg0*           | Checks if the flag listed in *cond_arg0* is `OFF`. |

::end-spantable::

#### Do Types
Some observer *do_type* can turn a flag `ON`.

::spantable::

| Do Type # | Class Name       | observerinfo Field | Class Name                                                                                   |
| --------- | ---------------- | ------------------ | -------------------------------------------------------------------------------------------- |
| 3         | SaEnTelephone    | arg0, arg1         | If the flag in arg1 is turned `ON`, then turned `OFF`, the flag in arg0 will be turned `ON`. |
| 7         | EnSetEventFlagOn | arg0               | Turns `ON` the flag listed in arg0.                                                          |
|           |                  |                    |                                                                                              |
::end-spantable::

#### Move Types
Some furnitureinfo *move* types can turn a flag `ON`.

::spantable::

| Move<br>Type # | Behavior              | Furnitureinfo<br>Fields Used | Description                                                                               |
| -------------- | --------------------- | ---------------------------- | ----------------------------------------------------------------------------------------- |
| 16             | Books                 | arg0 @span                   | When Luigi interacts with the furniture, the flag in arg0 will then be turned `ON`. @span |
| 33             | Button                |                              |                                                                                           |
| 43             | Angel Statue          |                              |                                                                                           |
| 38             | Furniture with a Door | arg0, arg1                   | If arg0 = 1, the furniture will turn the flag listed in arg1 `ON` when opened.            |
|                |                       |                              |                                                                                           |
|                |                       |                              |                                                                                           |

::end-spantable::
