Torch with OpenMP support...on *OS X!*
============
Sometimes, you just can't get that neural network crammed into the seemingly ever-inadequate GPU VRAM.  Sometimes, your network just *needs* to be balls wide and nut deep.  Sometimes, you had to buy a car instead of a workstation with four of [these](http://www.newegg.com/Product/Product.aspx?Item=N82E16814132041), but also want to test something from home without begging for time on the university cluster.  (DAT CLUSTER ლ(·̿̿益·̿̿ヽ)ლ though.) 

4GB is what people will say is the minimum (kind of like the people who say you can subsist on minimum wage).  8GB is....less inadequate.  

What if you need 30GB? Bust out that Xeon CPU, cause we're gonna use your *actual* RAM.  And swap I guess, if you just want to watch the world burn. 

This ultra niche repo lets you do that - on OS X.  This is the main torch distro with very minor modifications to the build scripts so it will automatically install a more recent version of clang (but stowed safely out of your paths) that supports OpenMP.  Ever seen LuaJIT use 6000% CPU? You will with this! (CPU core count permitting).

Oh, and since nvcc is a picky little bitch (at least on OS X) and refuses to work with pretty much every -ccbin except like 2 random versions of clang that were made in the 1970s and came on 8" floppies**&dagger;**, the build script deals with that too.  

Anyway, as near as I can tell, nvcc works fine with most of what it says it won't, just make sure you never tell it what your cc binary is and problem solved!
###### &dagger; statement might be bullshit.
-------------------------
Install dependencies. Uses `brew` on OSX.
```sh
curl -s https://raw.githubusercontent.com/metacollin/distro/master/install-deps | bash
```

Install this repo, which installs the torch distribution, with a lot of nice goodies.
```sh
git clone https://github.com/metacollin/distro.git ~/torch --recursive
cd ~/torch; ./install.sh
```

By default Torch will install LuaJIT 2.1. If you want other options, you can use the command:
```sh
TORCH_LUA_VERSION=LUA51 ./install.sh
TORCH_LUA_VERSION=LUA52 ./install.sh
```

Now, everything should be installed. Either open a new shell, or source your profile via
```sh
. ~/.bashrc  # or: . ~/.zshrc
th -e "print 'I just installed Torch! Awwww yisssss.'"
```

Note: If you use a non-standard shell, you'll want to run this command
```sh
./install/bin/torch-activate
```

Tested on OSX 10.11.6.
