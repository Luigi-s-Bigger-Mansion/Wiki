### **Description**

Flags are boolean (`ON`/`OFF`) variables that help the game keep track of progress.<br>
There are 255 flags in the game, each with different saving properties that can be divided into one of three groups: Savable Flags, Room Flags, and Map Flags.

!!! info "Types of Flags"

	=== "Savable Flags<br>(1-84)"
		Once these flags are turned `ON`, they will stay `ON`. The state of these flags can be saved to the memory card.

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

The status of these flags can be checked with Events, JMP Tables, and ASM.<br>
The table below lists all 255 flags and what they are tied to.

### How to Change Flag Status

### How to Check Flags

## Savable Flags

::spantable:: class=":white_check_mark:"

| Flag # | Flag Tied to JMP? | Flag Tied to Events? | Flag Tied to ASM? |
| ------ | ----------------- | -------------------- | ----------------- |
| 0      |                   |                      | :x:               |
| 1      | :x:               | :x:                  | :x:               |
| 2      | :x:               | :x:                  |                   |
| 3      | :x:               | :x:                  | :x:               |
| 4      | :x:               | :x:                  | :x:               |
| 5      |                   | :x:                  | :x:               |
| 6      | :x:               | :x:                  | :x:               |
| 7      |                   | :x:                  | :x:               |
| 8      |                   | :x:                  |                   |
| 9      |                   | :x:                  |                   |
| 10     | :x:               | :x:                  |                   |
| 11     | :x:               | :x:                  |                   |
| 12     | :x:               |                      | :x:               |
| 13     | :x:               | :x:                  |                   |
| 14     | :x:               |                      |                   |
| 15     | :x:               | :x:                  | :x:               |
| 16     |                   | :x:                  |                   |
| 17     | :x:               | :x:                  | :x:               |
| 18     | :x:               | :x:                  | :x:               |
| 19     | :x:               | :x:                  |                   |
| 20     |                   | :x:                  |                   |
| 21     | :x:               | :x:                  | :x:               |
| 22     | :x:               | :x:                  | :x:               |
| 23     |                   | :x:                  |                   |
| 24     | :x:               | :x:                  | :x:               |
| 26     |                   | :x:                  |                   |
| 27     | :x:               | :x:                  | :x:               |
| 29     |                   | :x:                  |                   |
| 30     | :x:               | :x:                  | :x:               |
| 32     |                   | :x:                  |                   |
| 33     | :x:               | :x:                  | :x:               |
| 35     | :x:               | :x:                  |                   |
| 36     | :x:               |                      | :x:               |
| 37     | :x:               | :x:                  |                   |
| 38     | :x:               | :x:                  |                   |
| 39     | :x:               | :x:                  | :x:               |
| 40     | :x:               | :x:                  | :x:               |
| 41     | :x:               |                      | :x:               |
| 42     |                   | :x:                  |                   |
| 43     | :x:               |                      | :x:               |
| 44     | :x:               |                      | :x:               |
| 45     | :x:               |                      | :x:               |
| 46     | :x:               | :x:                  | :x:               |
| 47     | :x:               |                      | :x:               |
| 48     |                   |                      | :x:               |
| 49     | :x:               |                      | :x:               |
| 50     | :x:               | :x:                  | :x:               |
| 51     | :x:               |                      | :x:               |
| 52     | :x:               | :x:                  |                   |
| 53     |                   | :x:                  |                   |
| 54     | :x:               | :x:                  |                   |
| 55     | :x:               |                      | :x:               |
| 56     | :x:               | :x:                  | :x:               |
| 57     | :x:               | :x:                  |                   |
| 58     |                   | :x:                  |                   |
| 59     | :x:               | :x:                  |                   |
| 61     | :x:               | :x:                  | :x:               |
| 62     | :x:               |                      | :x:               |
| 63     | :x:               | :x:                  | :x:               |
| 64     |                   |                      | :x:               |
| 65     |                   | :x:                  | :x:               |
| 66     | :x:               | :x:                  | :x:               |
| 67     | :x:               | :x:                  | :x:               |
| 68     | :x:               | :x:                  | :x:               |
| 69     |                   | :x:                  |                   |
| 70     | :x:               |                      |                   |
| 71     |                   | :x:                  |                   |
| 72     | :x:               |                      |                   |
| 73     | :x:               | :x:                  |                   |
| 74     | :x:               | :x:                  | :x:               |
| 75     | :x:               | :x:                  | :x:               |
| 76     | :x:               |                      |                   |
| 77     | :x:               | :x:                  |                   |
| 78     |                   |                      | :x:               |
| 79     |                   |                      | :x:               |
| 80     | :x:               |                      | :x:               |
| 81     | :x:               | :x:                  | :x:               |
| 82     | :x:               | :x:                  | :x:               |
| 83     | :x:               | :x:                  | :x:               |
| 84     |                   | :x:                  |                   |

::end-spantable::
