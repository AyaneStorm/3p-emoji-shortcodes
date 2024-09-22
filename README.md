# 3p-emoji-shortcodes
Does not replace :-P and :-D with nonsensical emojis

You'll need Facebook archiver ZSTD to compress back to a .zst file. You can find it here: https://github.com/facebook/zstd
Compile ZSTD in Cygwin and make the compiled zstd executable available in your PATH.

If you need to remove other emojis:

1. Clone this repository
2. Make your modifications
3. Type the following commands:

```
cd /cygdrive/c/path/to/3p-emoji-shortcodes/
find /cygdrive/c/path/to/3p-emoji-shortcodes/emoji_shortcodes-15.3.2.10207138275-common-10207138275/ -printf "%P\n" | tar -cf emoji_shortcodes-15.3.2.10207138275-common-10207138275.tar --no-recursion -C /cygdrive/path/to/3p-emoji-shortcodes/emoji_shortcodes-15.3.2.10207138275-common-10207138275/ -T -
zstd emoji_shortcodes-15.3.2.10207138275-common-10207138275.tar -o emoji_shortcodes-15.3.2.10207138275-common-10207138275.tar.zst
md5sum emoji_shortcodes-15.3.2.10207138275-common-10207138275.tar.zst
```

Then in your Firestorm autobuild.xml (or my_autobuild.xml if you have one), find the emoji_shortcodes key and replace values with this:

```
              <key>hash</key>
              <string>result of the md5sum command you ran earlier (for example 03780bbf62aa4eb324c9fb7872633528)</string>
              <key>hash_algorithm</key>
              <string>md5</string>
              <key>url</key>
              <string>file:///C:/path/to/3p-emoji-shortcodes/emoji_shortcodes-15.3.2.10207138275-common-10207138275.tar.zst</string>
```

Then delete the packages directory in your build-vc170-64 directory, then reconfigure and rebuild your Firestorm.