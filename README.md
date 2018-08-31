# cryptopals
https://cryptopals.com

bash

1.
1.1
<pre>
echo "4927606b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d" |xxd -r -p|openssl base64
</pre>
1.2
<pre>
echo -n 1c0111001f010100061a024b53535009181c >b1.txt
cat b1.txt |perl -ne '$b="686974207468652062756c6c277320657965"; @b2=( $b =~ m/(..)/g ); @b1=(m/(..)/g ); for($i=0;$i<18;$i++) {print chr( hex($b2[$i])^hex($b1[$i]) )}; print chr 10'
</pre>

1.3
<pre>
echo -n 1b37373331363f78151b7f2b783431333d78397828372d363c78373e783a393b3736 >c1.txt
cat c1.txt |perl -ne ' @b1=(m/(..)/g ); for($i=0;$i<length($_)/2;$i++) {print $b1[$i].chr 10;}'|sort |uniq -c|sort -n
ETAOIN SHRDLU
      1 15
      1 28
      1 2b
      1 2d
      1 34
      1 3a
      1 3b
      1 3c
      1 3d
      1 3e
      1 3f
      1 7f
      2 1b
      2 31
      2 33
      2 39
      3 36
      5 37
      6 78

cat c1.txt |perl -ne ' @b1=(m/(..)/g ); for($z=0;$z<256;$z++) { print $z." "; for($i=0;$i<length($_)/2;$i++) {print chr($z^hex($b1[$i]));} print chr 10;}'
cat c1.txt |perl -ne ' @b1=(m/(..)/g ); for($z=0;$z<256;$z++) { print $z." "; for($i=0;$i<length($_)/2;$i++) {$p=chr($z^hex($b1[$i])); print $p if(ord($p)<128 && ord($p)>31);} print chr 10;}'
88 Cooking MC's like a pound of bacon
</pre>

1.4
<pre>
wget https://cryptopals.com/static/challenge-data/4.txt
cat 4.txt |perl -ne 'chomp;@b1=(m/(..)/g ); for($z=0;$z<256;$z++) {$l=""; for($i=0;$i<length($_)/2;$i++) {$p=chr($z^hex($b1[$i]));  $l.=$p if(ord($p)<128 && ord($p)>31);} if(length($l)>28){print $z." ".$_." ".$l.chr(10);} }'|grep -i the
53 7b5a4215415d544115415d5015455447414c155c46155f4058455c5b523f Now that the party is jumping
</pre>

1.5
<pre>
#!/usr/bin/perl -w

use strict;
my $key="ICE";
my @k=split(//,$key);
my $i=0;

while(<>)
{
        my @l=split(//);
        foreach my $c (@l){
                printf("%02x", ord($k[$i])^ord($c));
                $i++;
                $i=0 if($i>=length($key));
        }
}
print "\n";
</pre>
1.6
