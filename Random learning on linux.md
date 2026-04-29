
Random llearnign on linux: 
16th Jan 2026
- journalctl
- systemctl 
- fd
  examples:
  systemctl list-unit-files --state=enabled --type=service --no-pager
  fd -e service . ~/.config/
  
- log
  
#+begin_src text
ps aux                     # All processes
ps -ef                     # All processes (different format)
ps -eo pid,user,cmd        # Custom output
top                        # Real-time process viewer
htop                       # Better interactive process viewer

#+end_src

* Rsync
rsync -avP folder/ user@host:/path/

* Image resizer
Mon Mar  2 19:31:35 2026
magick wallpaper-513.jpg -resize 400x400^ -gravity center -extent 400x400 -quality 85 isha.jpg

* Removing packages
pacman -Rps  .... -p 
sudo pacman -Rns ... 
pacman -Qdtq | sudo pacman -Rs -

* Create a file for testing filled with zeros and size
dd if=/dev/zero of=/tmp/bigfile.dat bs=1M count=4096 

This command creates a 4GB file filled with zeros. Here's the breakdown:
dd — "disk/data duplicator", a low-level data copying utility.
PartMeaningif=/dev/zeroInput file = /dev/zero, a special Linux device that produces an infinite stream of null bytes (zeros)of=bigfile.datOutput file = bigfile.dat, the file being created in the current directorybs=1MBlock size = 1 Megabyte per read/write operationcount=4096Number of blocks to copy = 4096
Total size = 1M × 4096 = 4096 MB = 4 GB

Common uses for this pattern:

Benchmarking disk write speed — see how fast your storage can write sequential data
Creating a test file — to fill a partition, simulate load, or test a filesystem
Zeroing out space — before encryption or secure deletion
Creating swap files or disk images — pre-allocating a fixed-size file
