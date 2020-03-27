---
draft: false
date: 2014-10-30
layout: post
title: Converting DNG to jpeg
tags: raw, dng, pictures, btsync, scripting
---

I shoot most of my pictures in RAW with my Nikon D90. Once I transfer them to my computer, I change the format to DNG (I am not sure if this is useful or not, but NEF is Nikon's proprietary format whereas DNG is standard, backed by Adobe and -in theory- future proof). However, raw formats are not useful for quick previewing and most machines do not support it natively (Macs do support it, though).

Then all my pictures are kept in a hard drive that syncs to some computers using [bittorrent sync](https://www.bittorrent.com/sync/). One of the copies is a HTPC that I have connected to my home TV, so it serves both as a backup in case the hard drive where the pictures are kept is lost or stolen and as a way to see them comfortably in the TV. This is where a script that transforms raw images into jpeg comes handy.

This script uses [dcraw](https://www.cybercom.net/~dcoffin/dcraw/) and I have used info from [here](https://stackoverflow.com/questions/8699293/how-to-monitor-a-complete-directory-tree-for-changes-in-linux) and [here](https://www.mutaku.com/wp/index.php/2011/02/cook-your-raw-photos-into-jpeg-with-linux/).

Check it out [here](https://gist.github.com/frosklis/466a77f2c9972990a141). There are things missing, such as real file change monitoring, but it gets the job done.
<pre><code>
#!/bin/bash

export current=`pwd`
export rawfolder=/home/claudio/sync/fotos
echo $current
echo $rawfolder

# list of directories
# cd "$rawfolder" && find . \( ! -regex '.*/\..*' \) -type d -newer old_dirs.txt > "$current/dirs.txt" && cd "$current"
cd "$rawfolder" && find . \( ! -regex '.*/\..*' \) -type d > "$current/dirs.txt" && cd "$current"
cp dirs.txt old_dirs.txt

while read folder
do
	# echo converting pictures in "$rawfolder/$folder"
	mkdir -p "$folder"
	ls "$rawfolder/$folder/" > files.txt
	while read i
	# for i in "$rawfolder/$folder/*"
	do
		# if dng, convert else copy
		if [[ -f "$rawfolder/$folder/$i" ]]; then
			echo "$rawfolder/$folder/$i"
			if echo "$i" | grep -q '.dng$'; then
				dcraw -c "$rawfolder/$folder/$i" | cjpeg -quality 90 -optimize -progressive > "$folder/$(echo $(basename "$i" ".dng").jpg)"
			elif echo "$i" | grep -q '.jpg$'; then
				cp "$rawfolder/$folder/$i" "$folder/$i"
			fi
		fi
	done < files.txt
done < dirs.txt

echo Done.
</code></pre>