# memimgkcdump

I forked this project in order to make use of the output to [volafox project](http://code.google.com/p/volafox)

memimgkcdump is a proof-of-concept tool for 'keychaindump' function on volafox. output of volafox, master key candidates, uses them to decrypt keychain files.

Main writer's article(keychaindump) see the [blog post](http://juusosalonen.com/post/30923743427/breaking-into-the-os-x-keychain).

## How?
Build instructions:

    $ gcc memimgkcdump.c -o memimgkcdump -lcrypto

Basic usage:
    $ python vol.py -i [memory image] -o keychaindump
    ....
    [*] master key candidate: 9AB40E7378E195335019C5A3577123D5AC814C7D22588B2F
    
    $ ./memimgkcdump [master key candidate] [path to keychain file]

Example with truncated and censored output:

    $ python vol.py -i [memory image] -o keychaindump

	[+] Virtual Memory Map Information
	 [-] Virtual Address Start Point: 0x1099e1000
	 [-] Virtual Address End Point: 0x7fffffe00000
	 [-] Number of Entries: 92
	
	[+] Generating Process Virtual Memory Maps
	 [-] Region from 0x1099e1000 to 0x109aea000 (r-x, max rwx;)
	 [-] Region from 0x109aea000 to 0x109af7000 (rw-, max rwx;)
	 ...
	 [-] Region from 0x10a072000 to 0x10a073000 (---, max rwx;)
	 [-] Region from 0x10a073000 to 0x10a0ce000 (rw-, max rwx;)
	 [-] Region from 0x10a0ce000 to 0x10b2f3000 (r--, max r-x;)
	 [-] Region from 0x7fedc9c00000 to 0x7fedc9d00000 (rw-, max rwx;)
	 [-] Region from 0x7fedc9d00000 to 0x7fedc9e00000 (rw-, max rwx;)
	 [-] Region from 0x7fedc9e00000 to 0x7fedc9f00000 (rw-, max rwx;)
	 [-] Region from 0x7fedca000000 to 0x7fedca0e5000 (rw-, max rwx;)
	 [-] Region from 0x7fedca0e5000 to 0x7fedca0e7000 (rw-, max rwx;)
	 [-] Region from 0x7fedca0e7000 to 0x7fedca0f8000 (rw-, max rwx;)
	 [-] Region from 0x7fedca0f8000 to 0x7fedca0fa000 (rw-, max rwx;)
	 [-] Region from 0x7fedca0fa000 to 0x7fedca800000 (rw-, max rwx;)
	 ...
	 [-] Region from 0x7fff7a000000 to 0x7fff7a200000 (rw-, max rwx;)
	 [-] Region from 0x7fff7a200000 to 0x7fff7a26e000 (rw-, max rwx;)
	 [-] Region from 0x7fff7a26e000 to 0x7fff80000000 (r--, max rwx;)
	 [-] Region from 0x7fff80000000 to 0x7fffc0000000 (r--, max rwx;)
	 [-] Region from 0x7fffc0000000 to 0x7fffffe00000 (r--, max rwx;)
	 [-] Region from 0x7fffffe00000 to 0x7fffffe01000 (r--, max r--;)
	 [-] Region from 0x7ffffffca000 to 0x7ffffffcb000 (r-x, max r-x;)
	
	[+] Find MALLOC_TINY heap range (guess)
	 [-] range 0x7fedc9c00000-0x7fedc9d00000
	 [-] range 0x7fedc9d00000-0x7fedc9e00000
	 [-] range 0x7fedc9e00000-0x7fedc9f00000
	 [-] range 0x7fedcb000000-0x7fedcb100000
	 [-] range 0x7fedcb100000-0x7fedcb200000
	 [-] range 0x7fedcb200000-0x7fedcb300000
	
	[*] Search for keys in range 0x7fedc9c00000-0x7fedc9d00000 complete. master key candidates : 4
	[*] Search for keys in range 0x7fedc9d00000-0x7fedc9e00000 complete. master key candidates : 4
	[*] Search for keys in range 0x7fedc9e00000-0x7fedc9f00000 complete. master key candidates : 4
	[*] Search for keys in range 0x7fedcb000000-0x7fedcb100000 complete. master key candidates : 5
	[*] Search for keys in range 0x7fedcb100000-0x7fedcb200000 complete. master key candidates : 5
	[*] Search for keys in range 0x7fedcb200000-0x7fedcb300000 complete. master key candidates : 5
	
	[*] master key candidate: ACEFBB5CECE8398E780016DAF685E39A8E36FDE8EC8B6B6E
	[*] master key candidate: C7A8DC12E05F1BEEF70228C304E6567CFDA07BEAB86606C7
	[*] master key candidate: E340E90C2EC1E55BC116A2775624FC3D4ADD35E248E543C1
	[*] master key candidate: 9AB40E7378E195335019C5A3577123D5AC814C7D22588B2F
	[*] master key candidate: 9AB40E7378E195335019C5A3577123D5AC814C7D22588B2F

    $ sudo ./memimgkcdump E340E90C2EC1E55BC116A2775624FC3D4ADD35E248E543C1 login.keychain
    [*] Trying to decrypt wrapping key in login.keychain
	[*] Trying master key candidate: E340E90C2EC1E55BC116A2775624FC3D4ADD35E248E543C1
	[+] Found master key: E340E90C2EC1E55BC116A2775624FC3D4ADD35E248E543C1
	[+] Found wrapping key: 9ab40e7378e195335019c5a3577123d5ac814c7d22588b2f
	xxxxx@live.com:pop3.live.com:xxxxx
	xxxxxx@live.com:smtp.live.com:xxxxxxx
    ...

## Who?
Keychaindump was modified by [n0fate](http://twitter.com/n0fate)

and

Keychaindump was written by [Juuso Salonen](http://twitter.com/juusosalonen), the guy behind [Radio Silence](http://radiosilenceapp.com) and [Private Eye](http://radiosilenceapp.com/private-eye).

## License
Do whatever you wish. Please don't be evil.