sqlite-autoconf-3070800
=======================

sqlite-sources-mac

http://stackoverflow.com/questions/7368392/help-to-fix-strange-sqlite3-error-dyld-library-not-loaded-usr-lib-libsqlite


2
down vote
favorite
3
I am suddenly getting an sqlite3 error:

ActionView::Template::Error (dyld: Library not loaded: /usr/lib/libsqlite3.0.dylib
Referenced from: /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/CFNetwork.framework/Versions/A/CFNetwork
Reason: no suitable image found.  Did find:
        /usr/lib/libsqlite3.0.dylib: mach-o, but wrong architecture
        /usr/local/lib/libsqlite3.0.dylib: mach-o, but wrong architecture
        /usr/lib/libsqlite3.0.dylib: mach-o, but wrong architecture
I have no idea why I am suddenly getting this error. Rails 3.1.0 and Ruby 1.9.2 Mac OSX 10.5.8

sqlite3 ruby-on-rails-3.1 osx-leopard
share|improve this question
edited Sep 9 '11 at 23:19

asked Sep 9 '11 at 23:11

Richard Jordan
3,77511736
add comment
3 Answers
activeoldestvotes
up vote
5
down vote
accepted
Okay so this is a messed up sqlite3 install and it seems that lots of people run into this problem but solutions are a little hard to come by. After a lot of googling I did the following:

Step1: went to http://www.sqlite.org/download.html and downloaded sqlite-autoconf-3070800.tar.gz under source code

Step2: expand file and cd into the resultant directory

Step3: sudo CFLAGS='-arch i686 -arch x86_64' LDFLAGS='-arch i686 -arch x86_64' ./configure --disable-dependency-tracking

Step4: sudo make install

Step5: added /usr/local/lib to the path

I was doing an awful lot of tinkering during this time. It's possible that I have done something else along the way and not realized and not included it here. But these steps seemed to fix the problem for me.

My environment: Mac OSX 10.5.8 MacBookPro4, Intel Core 2 Duo, 2.5 GHz

share|improve this answer
answered Oct 22 '11 at 23:46

Richard Jordan
3,77511736
add comment

up vote
4
down vote
Thank you so much, in my case I had to rearrange the parameters and I didn't use sudo to configure nor to make:

make clean

./configure --disable-dependency-tracking --prefix=/usr CFLAGS='-arch i686 -arch x86_64' LDFLAGS='-arch i686 -arch x86_64'

make

sudo make install

I didn't have to modify the path, I specified in the --prefix="my path"

Environment Mac OS X v.10.5.8 2GHz Intel Core 2 Duo
