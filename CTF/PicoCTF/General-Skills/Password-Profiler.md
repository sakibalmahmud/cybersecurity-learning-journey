Password-Profiler.md

View user information:

cat userinfo.txt

Generate custom wordlist:

cupp -i

Check generated files:

ls -lh

head -20 alice.txt

Crack SHA1 hash:

john --format=Raw-SHA1 --wordlist=alice.txt hash.txt.1

Display cracked password:

john --show --format=Raw-SHA1 hash.txt.1

Update Python script:

nano check_password.py
