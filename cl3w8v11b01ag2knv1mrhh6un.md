## Bash Script That Prints All Possible Combinations Of Two Letters

This is quite an interesting task, and the solution to it introduces a very important concept in Linux and shell scripting.

In one of the projects that we undertook today, we were to write a bash script that
prints all possible combinations (with a particular exception) of two letters.

So, let's take a practical example of this problem for the purposes of this tutorial.

```
Create a script that prints all possible combinations of two letters, except ee
- Letters are lower cases, from a to z
- One combination per line
- The output should be alpha ordered, starting with aa
- Do not print ee
```

To be able to solve the problem above, we would have to understand how we can combine letters in Linux.

## How to combine letters in Linux
The easiest way to this is to use the brace expansion. This is also another form of the shell expansions and can help you achieve a number of interesting outcomes. 

To understand what shell expansions are, check out my previous article on the topic: 
[Shell Expansions in Linux: What it means and how to take advantage of it](https://medium.com/@ehoneahobed/shell-expansions-in-linux-what-it-means-and-how-to-take-advantage-of-it-41d471cb02dc)

With brace expansion, you can create or generate lists with specific patterns. In our case, we want to use the brace expansion to generate a list of letter combinations (2 each).

## What is brace expansion
As stated in the previous article, shell expansions are shorthands that the shell terminal understands and will usually interpret before running any commands given to it.

Brace expansions consist of an expression that is contained in curly brackets `{}`. The expression inside the curly bracket can be a list of comma separated values or a given range.

For example `{1,2,3,4}`, `{1..10}`, `{a,b,c,d}`, `{obed, frank, felix, pascal}`.

Any time you pass any of the above examples or something similar to a shell command as an argument, an expansion takes place and the outcome is that each member of the list or range will be submitted to the command as an individual argument for it to be evaluated.

This means that a command like
```
echo {1,2,3,4}
```

will pass each member of the list to the echo command during the expansion. So behind the scene the shell terminal will be doing something as below but not show it to us:
```
echo 1
echo 2
echo 3
echo 4
```

As such we get the output to be
```
1 2 3 4
```
That is the concept of brace expansion. However, implementation of the brace expansion can be far more complex and intuitive than this. One such case which makes brace expansion an important concept is the concatenation and nesting of braces.

## How to use concatenation and nesting of braces 
When you put one brace `{1,2,3}` adjacent to another brace `{a,b,c}`, you get an interesting output and that is the concept that will help us solve the practical problem we have at hand.

With the adjacent braces, each element in one of the braces is acted upon by all elements in the other brace.

For example:
```
echo {1,2,3}{a,b,c}
```

will give an output of
```
1a 1b 1c 2a 2b 2c 3a 3b 3c
```
This is like doing some sort of multiplication where each member of the first brace will multiply all the members in the second brace.

Therefore, if we want a combination of letters like the question is requiring of us then we would have to provide the range of letters as two adjacent braces to be expanded `{a..z}{a..z}`

NB: The shell understands ranges defined by the first and last number separated by two dots. What `{a..z}` means is that, give the range from a to z in lower case letters

```
echo {a,b,c}
a b c d e f g h i j k l m n o p q r s t u v w x y z
```

## How to combine letters in shell
Now that we understand the basis of brace expansion, let's go ahead to answer our question.

If I want to print the combination of two letters of the alphabets in lower cases then I will issue the command below:

```
echo {a..z}{a..z}
```
which will give you an output of

```
aa ab ac ad ae af ag ah ai aj ak al am an ao ap aq ar as at au av aw ax ay az ba bb bc bd be bf bg bh bi bj bk bl bm bn bo bp bq br bs bt bu bv bw bx by bz ca cb cc cd ce cf cg ch ci cj ck cl cm cn co cp cq cr cs ct cu cv cw cx cy cz da db dc dd de df dg dh di dj dk dl dm dn do dp dq dr ds dt du dv dw dx dy dz ea eb ec ed ee ef eg eh ei ej ek el em en eo ep eq er es et eu ev ew ex ey ez fa fb fc fd fe ff fg fh fi fj fk fl fm fn fo fp fq fr fs ft fu fv fw fx fy fz ga gb gc gd ge gf gg gh gi gj gk gl gm gn go gp gq gr gs gt gu gv gw gx gy gz ha hb hc hd he hf hg hh hi hj hk hl hm hn ho hp hq hr hs ht hu hv hw hx hy hz ia ib ic id ie if ig ih ii ij ik il im in io ip iq ir is it iu iv iw ix iy iz ja jb jc jd je jf jg jh ji jj jk jl jm jn jo jp jq jr js jt ju jv jw jx jy jz ka kb kc kd ke kf kg kh ki kj kk kl km kn ko kp kq kr ks kt ku kv kw kx ky kz la lb lc ld le lf lg lh li lj lk ll lm ln lo lp lq lr ls lt lu lv lw lx ly lz ma mb mc md me mf mg mh mi mj mk ml mm mn mo mp mq mr ms mt mu mv mw mx my mz na nb nc nd ne nf ng nh ni nj nk nl nm nn no np nq nr ns nt nu nv nw nx ny nz oa ob oc od oe of og oh oi oj ok ol om on oo op oq or os ot ou ov ow ox oy oz pa pb pc pd pe pf pg ph pi pj pk pl pm pn po pp pq pr ps pt pu pv pw px py pz qa qb qc qd qe qf qg qh qi qj qk ql qm qn qo qp qq qr qs qt qu qv qw qx qy qz ra rb rc rd re rf rg rh ri rj rk rl rm rn ro rp rq rr rs rt ru rv rw rx ry rz sa sb sc sd se sf sg sh si sj sk sl sm sn so sp sq sr ss st su sv sw sx sy sz ta tb tc td te tf tg th ti tj tk tl tm tn to tp tq tr ts tt tu tv tw tx ty tz ua ub uc ud ue uf ug uh ui uj uk ul um un uo up uq ur us ut uu uv uw ux uy uz va vb vc vd ve vf vg vh vi vj vk vl vm vn vo vp vq vr vs vt vu vv vw vx vy vz wa wb wc wd we wf wg wh wi wj wk wl wm wn wo wp wq wr ws wt wu wv ww wx wy wz xa xb xc xd xe xf xg xh xi xj xk xl xm xn xo xp xq xr xs xt xu xv xw xx xy xz ya yb yc yd ye yf yg yh yi yj yk yl ym yn yo yp yq yr ys yt yu yv yw yx yy yz za zb zc zd ze zf zg zh zi zj zk zl zm zn zo zp zq zr zs zt zu zv zw zx zy zz
```
We have gotten the combination of letters but with our question, there has to be an exception. So, instead of printing everything, we have to print all with the exception of ee.

How do we go about that?

## How to exclude something from an output in Linux
This can be achieved with a shell command that allows us to search for specified patterns. The `grep` command is used to search for patterns that we pass to it as attributes.

This means that we can pass `ee` as an attribute to the `grep` command if what we are searching for is `ee`. In such a situation, the shell will output the patern `ee` or any set of words that contain the `ee` pattern.

However, in this specific case, we are not interested in the pattern `ee`. We rather want to exclude it from our output. To achieve something like that, we have to introduce the `-v` option to the `grep` command.

Also, since we are searching for the output of an `echo` command, we have to pass that output to the `grep` command as the attribute. The concept of [piping (|)](https://www.geeksforgeeks.org/piping-in-unix-or-linux/#:~:text=A%20pipe%20is%20a%20form,program%2Fprocess%20for%20further%20processing.) will therefore be applied here

Let's take an example.
```
echo -e "My name is Ehoneah Obed \n I am currently studying Software Engineering at ALX \n I am glad"
```
The echo statement above prints 3 different lines. This is because the option `-e` tells the echo command to interpret the escape sequence `\n` which means 'go to next line'

The outcome of that command is:
```
My name is Ehoneah Obed 
 I am currently studying Software Engineering at ALX 
 I am glad

```
We can go ahead to pass the outcome to the `grep` command with the help of a pipline `|`. The command then looks like this:
```
echo -e "My name is Ehoneah Obed \n I am currently studying Software Engineering at ALX \n I am glad" | grep e
```

The output of the above command is 
```
My name is Ehoneah Obed 
I am currently studying Software Engineering at ALX
```
Wait! How come only two lines were printed?

Oh yeah, that wasn't a mistake. The `grep` command was supposed to search and display all lines containing an `e`. Unfortunately, the last line didn't contain an `e` hence it wasn't printed out.

In the same way we can decide to print all lines except those that contain the letter `e`. This is where we pass the `-v` option to the `grep` command. The new command will therefore be:
```
echo -e "My name is Ehoneah Obed \n I am currently studying Software Engineering at ALX \n I am glad" | grep -v e
```
The output of the above command is:
```
I am glad
```
The first two lines were ignored and not printed because both of them had the letter `e` in them.

## Solution: Print all combination of the letters except `ee`
The initial output of the letter combinations had each combination separated by a space and hence the shell will consider it as a single line of text as we saw in the output provided earlier.

This means that if we go ahead and pass the the outcome to the `grep -v ee` command with the help of a pipeline `|`, nothing will be returned.

Let's give it a try.

```
echo {a..z}{a..z} | grep -v ee
```
The command above returns nothing as you can see below:
```

```
This is because the output of the first expression `echo {a..z}{a..z}` is seen as one line and that line has `ee` in it so the `grep -v ee` command tells shell to ignore it.

Hence, to get the right answer, we have to find a way to have the output of the first expression to be printed with each letter combination on a separate line.

In fact, the preamble to the question we are answering mentioned that we should have one combination per line.

How can we achieve that? Think hard.

Well there is another shell command that can help us to that. The translate `tr` command is what we are going to use.

This command is used to translate (meaning replace something with something else). This is like saying where ever you see one thing replace it with another.

This is done in our normal lives. For instance, I can decide to replace `Thank You` with `Merci` which is the French translation of the English word. I hope you get it?

Now, let's see how you can use the `tr` command to achieve the result we are looking for.

Since, we currently have each letter combination pair being separated by a space, we can replace that space with a new line.

In the shell, a new line is represented by `'\n'` whiles a space is represented by `' '`. So, we can translate them by using the command below:
```
tr ' ' '\n'
```

We can therefore pass the outcome of the letter combination as arguments for the `tr` command with the help of a pipeline and then pass the net outcome as arguments for the `grep -v ee` command.

The final command therefore looks like:
```
echo {a..z}{a..z} | tr ' ' '\n' | grep -v ee
```
The output is a long list of all the letter combinations with each pair on a single line with the exception of `ee` which doesn't appear at all.

```
aa
ab
ac
ad
ae
af
ag
ah
ai
aj
ak
al
am
an
ao
ap
aq
ar
as
at
au
av
aw
ax
ay
az
ba
bb
bc
bd
be
bf
bg
bh
bi
bj
bk
bl
bm
bn
bo
bp
bq
br
bs
bt
bu
bv
bw
bx
by
bz
ca
cb
cc
cd
ce
cf
cg
ch
ci
cj
ck
cl
cm
cn
co
cp
cq
cr
cs
ct
cu
cv
cw
cx
cy
cz
da
db
dc
dd
de
df
dg
dh
di
dj
dk
dl
dm
dn
do
dp
dq
dr
ds
dt
du
dv
dw
dx
dy
dz
ea
eb
ec
ed
ef
eg
eh
ei
ej
ek
el
em
en
eo
ep
eq
er
es
et
eu
ev
ew
ex
ey
ez
fa
fb
fc
fd
fe
ff
fg
fh
fi
fj
fk
fl
fm
fn
fo
fp
fq
fr
fs
ft
fu
fv
fw
fx
fy
fz
ga
gb
gc
gd
ge
gf
gg
gh
gi
gj
gk
gl
gm
gn
go
gp
gq
gr
gs
gt
gu
gv
gw
gx
gy
gz
ha
hb
hc
hd
he
hf
hg
hh
hi
hj
hk
hl
hm
hn
ho
hp
hq
hr
hs
ht
hu
hv
hw
hx
hy
hz
ia
ib
ic
id
ie
if
ig
ih
ii
ij
ik
il
im
in
io
ip
iq
ir
is
it
iu
iv
iw
ix
iy
iz
ja
jb
jc
jd
je
jf
jg
jh
ji
jj
jk
jl
jm
jn
jo
jp
jq
jr
js
jt
ju
jv
jw
jx
jy
jz
ka
kb
kc
kd
ke
kf
kg
kh
ki
kj
kk
kl
km
kn
ko
kp
kq
kr
ks
kt
ku
kv
kw
kx
ky
kz
la
lb
lc
ld
le
lf
lg
lh
li
lj
lk
ll
lm
ln
lo
lp
lq
lr
ls
lt
lu
lv
lw
lx
ly
lz
ma
mb
mc
md
me
mf
mg
mh
mi
mj
mk
ml
mm
mn
mo
mp
mq
mr
ms
mt
mu
mv
mw
mx
my
mz
na
nb
nc
nd
ne
nf
ng
nh
ni
nj
nk
nl
nm
nn
no
np
nq
nr
ns
nt
nu
nv
nw
nx
ny
nz
oa
ob
oc
od
oe
of
og
oh
oi
oj
ok
ol
om
on
oo
op
oq
or
os
ot
ou
ov
ow
ox
oy
oz
pa
pb
pc
pd
pe
pf
pg
ph
pi
pj
pk
pl
pm
pn
po
pp
pq
pr
ps
pt
pu
pv
pw
px
py
pz
qa
qb
qc
qd
qe
qf
qg
qh
qi
qj
qk
ql
qm
qn
qo
qp
qq
qr
qs
qt
qu
qv
qw
qx
qy
qz
ra
rb
rc
rd
re
rf
rg
rh
ri
rj
rk
rl
rm
rn
ro
rp
rq
rr
rs
rt
ru
rv
rw
rx
ry
rz
sa
sb
sc
sd
se
sf
sg
sh
si
sj
sk
sl
sm
sn
so
sp
sq
sr
ss
st
su
sv
sw
sx
sy
sz
ta
tb
tc
td
te
tf
tg
th
ti
tj
tk
tl
tm
tn
to
tp
tq
tr
ts
tt
tu
tv
tw
tx
ty
tz
ua
ub
uc
ud
ue
uf
ug
uh
ui
uj
uk
ul
um
un
uo
up
uq
ur
us
ut
uu
uv
uw
ux
uy
uz
va
vb
vc
vd
ve
vf
vg
vh
vi
vj
vk
vl
vm
vn
vo
vp
vq
vr
vs
vt
vu
vv
vw
vx
vy
vz
wa
wb
wc
wd
we
wf
wg
wh
wi
wj
wk
wl
wm
wn
wo
wp
wq
wr
ws
wt
wu
wv
ww
wx
wy
wz
xa
xb
xc
xd
xe
xf
xg
xh
xi
xj
xk
xl
xm
xn
xo
xp
xq
xr
xs
xt
xu
xv
xw
xx
xy
xz
ya
yb
yc
yd
ye
yf
yg
yh
yi
yj
yk
yl
ym
yn
yo
yp
yq
yr
ys
yt
yu
yv
yw
yx
yy
yz
za
zb
zc
zd
ze
zf
zg
zh
zi
zj
zk
zl
zm
zn
zo
zp
zq
zr
zs
zt
zu
zv
zw
zx
zy
zz

```
Hence, that is the right solution to the problem.

### Conclusion
I hope this makes things clearer and you understand everything we did in order to arrive at the answer. If you have any questions, comment it below and I will respond to it. You can also make suggestions on how I can make such tutorialsbetter for you.

Thanks for reading and I will love to connect personally with you. If you are on Twitter then you can [send me a DM](obeds://twitter.com/ehoneah).