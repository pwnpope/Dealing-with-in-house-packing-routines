In RITsec CTF 2024 I was able to blood [playoff-rondo's](https://github.com/thisusernameistaken) car hacking challenge where we had to do a good amount of RE and then finally we were able to write to memory to "turn on the engine", if you'd like a more in-depth explination of the challenge and how I solved it checkout my video write up [here](https://www.youtube.com/watch?v=9QnElpVlcEw)

---

- Before getting started make sure to manually rebase the binary in your disassembler to the binary base you're debugging if PIE is enabled just use the base as seen in GDB via vmmap

---

### dealing with in-house packing routines:

- when dealing with jank binaries that have in house packing routines try to dump the memory within GDB after running through the routines to then output it back to your disassembler for better decompilation:
	- `dump binary memory binary.bin start_addr stop_addr`

![](https://i.imgur.com/8FRa1Kz.png)
- so in this example we would use: `dump binary memory out.bin 0xd6d437b000 0xd6d437f000` 

- before:
![](https://i.imgur.com/qwbZ3HL.png)

- after:
![](https://i.imgur.com/DZq2Pyh.png)


---

- (Added treat - had to do this in the CTF) Manually resolving got entries
	1) Rebase in binja
	2) Click through till you see the address its pointing to
	3) Telescope the address in gdb -> xinfo the pointer its pointing
	4) Grab the offset from libc and search for that offset in libc in binja
		- Then you will figure out what function it is :)
