## Crypto small steps

This challenge is part of the HTB Cyber Apocalypse CTF 2023. 
Link of the contest: https://ctf.hackthebox.com/event/details/cyber-apocalypse-2023-the-cursed-mission-821

The following files can be downloaded from the challenge:

![image](https://user-images.githubusercontent.com/100348014/227995007-5b422347-1f43-472b-8615-866c76bdd48a.png)

Connect to the docker with netcat:
``` bash
nc 10.10.1.104 4387
```
We get the `n`, `e` and the encrypted value from the server.
``` bash
N = 9393717354913033880647758958169592695034252044786406718411950693430128104905399598219139104358833598546627301534964430000848448618761713843533892645664693
```
``` bash
e = 3
``` 
``` bash
Encrypted flag = 70407336670535933819674104208890254240063781538460394662998902860952366439176467447947737680952277637330523818962104685553250402512989897886053 
``` 
We need now to decode the flag, the vulnerability here is that the exponent is very small (3). For that we can use a tool name RsaCtfTools: https://github.com/RsaCtfTool/RsaCtfTool.

We just have to specify the `-n`, `-e` parameters and `--uncipher` with our encrypted flag and wait a few minutes.

![image](https://user-images.githubusercontent.com/100348014/228000315-58f0c516-1d55-441e-8131-523155ab14d9.png)
``` bash
./RsaCtfTool.py -n 9393717354913033880647758958169592695034252044786406718411950693430128104905399598219139104358833598546627301534964430000848448618761713843533892645664693 -e 3 
--uncipher 70407336670535933819674104208890254240063781538460394662998902860952366439176467447947737680952277637330523818962104685553250402512989897886053 
```

The tool used euler theorem to solve it: https://en.wikipedia.org/wiki/Euler%27s_theorem

Here is the flag!

![image](https://user-images.githubusercontent.com/100348014/228001732-98875984-6bca-420b-ad36-504faa6daad5.png)
