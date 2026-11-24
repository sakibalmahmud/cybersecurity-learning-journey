Multimode.md

View and identify message:

cat message.txt

file message.txt

xxd -p message.txt

Decode Base64:

base64 -d message.txt > decoded1.txt

cat decoded1.txt

Decode Hex:

xxd -r -p decoded1.txt > decoded2.txt

cat decoded2.txt

URL decode + ROT13:

python3 -c "import urllib.parse,codecs; print(codecs.decode(urllib.parse.unquote(open('decoded2.txt').read().strip()), 'rot_13'))"
