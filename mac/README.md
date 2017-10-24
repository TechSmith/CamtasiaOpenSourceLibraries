## Mac Custom Build Instructions
### Cairo
- Download Cairo source code
- Run the following commands

```
./configure
make
```
The compiled libraries will be in

- libs are in src/.libs
- util/cairo-gobject/.libs
- util/cairo-script/.libs
- util/cairo-trace/.libs


### Pango
- Download Pango source code
- Run the following commands

```
./configure
make
```

- The compiled libraries will be in pango/.libs

- To rebuild the makefile after editing the configure.ac or makefile.am files run 

```
./autogen.sh
make
```
	
- To install the required dependandies for pango 1.36.8 you can run 
```
brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/d4e4ea84da725cd379c0ed8249838be59c8cc4ac/Formula/pango.rb
```

### libintl
- Download gettext source code
- Run the following commands

```
./configure
make
```
The libintl library will be in gettext-runtime/intl/.libs/

### glib
The build set up for glib is a little complicated. The easiest way is probably to use a tool called Homebrew (http://brew.sh/) and to create a custom Homebrew formula. You will need to install Homebrew before proceeding.

Next, you'll want to make a zip of the source code with the changes that you want to be in your custom glib build:

- Download the glib source code
- Make any modifications to the source code that you would like
- Zip up the glib source code (into something like glibModified.zip)
- (Optional) Calculate the SHA256 hash with:

```
shasum -a 256 glibModified.zip
```
   
Once you have your glibModified.zip and the optional SHA256 hash, it's time to create your custom Homebrew formula for glib:

```
cd /usr/local/Library/Formula
cp glib.rb glibcustom.rb
```	

In **glibcustom.rb**:

- Change the first line from "class Glib < Formula" to "class Glibcustom < Formula"
- Change url to point to a local file URL like file:///Users/yourusername/Desktop/glibCustom.zip
- (Optional) Change the SHA256 has to the one calculate above

Now that you have your custom Homebrew formula for glib, you can use Homebrew to build it for you:

```
brew install glibcustom --build-from-sources
```

Homebrew will build your custom glib library to /usr/local/Cellar/glib
