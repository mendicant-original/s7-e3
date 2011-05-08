# RMU SESSION 7 EXERCISE 3

If in doubt about how to submit, see SUBMISSION_GUIDELINES file.

In this exercise, we'll be decoding binary file formats and working 
together to try to find ways to make that job easier. Please keep the following
guidelines in mind while working on this problem.

## GUIDELINES

* One goal of this project is to at least partially decode a binary file format
  of your own choosing. Most document, image and audio formats have open 
  specifications that describe how the files are organized, so you may want to 
  start by looking at the specs for common formats and seeing which ones seem 
  accessible to you.

* If you've never worked with binary file formats, don't worry! They may seem
  cryptic, but basically, all they are is a way to pack data efficiently into a
  file. Extracting that data is easy with Ruby's pack() and unpack() methods, as
  long as you know how the file is structured and what the data types are for
  the fields you are decoding. You can also try using BitStruct:
  http://bit-struct.rubyforge.org/

* Note that many file formats try to keep everything at the byte level, making
  using pack() and unpack() possible. However, some formats have fields that
  must be interpreted on a bit-by-bit basis and those will need some bitmasking
  to operate.

* You are not expected to implement anywhere near a full decoder for any
  particular file format. However, you are expected to extract enough
  information for your tool to be useful for something non-trivial.

* Make sure to announce what format you are working on processing, no two 
  students may work on the same file format. Additionally, outline what
  information you plan to decode from the file so that we can review whether it
  sounds like a good fit for this project.

* You aren't necessarily expected to work with a format that hasn't been decoded
  in Ruby before, but you get some bonus points for attempting that.

* Once you have a fairly functional decoder, you are expected to share your
  results with other students and see if there are common tools that can be
  extracted to reduce the duplication of effort between your implementations.
  It's okay if we ultimately don't find anything, but with many people doing a
  similar task, it's possible that we'll run into an idea for a nice helper
  library.

* Those who have some experience in processing binary file formats are 
  encouraged to actively help out those that don't. But if the class as a whole
  is lacking in that kind of experience, feel free to ask me to help, you're
  not expected to have a background in this. I picked this problem specifically
  because it's one that many Ruby developers never end up learning about, and
  because it's much easier than it seems on the surface.

* Navigating specifications for binary file formats can be a pain. Try to think
  of what info you might want to extract BEFORE reading specs, rather than
  trying to learn the formats from the top-down.

## EXAMPLE

The following code demonstrates using unpack to extract the dimensions of a PNG file,
based on the specification at: http://www.w3.org/TR/PNG/#11IHDR

    >> File.binread("arrow.png").unpack("x16NN")
    => [42, 23]

If we wanted to see a bit more of what was going on, we could pull the PNG
string out of the signature on the file, as well as the identifier for the
chunk that the dimensions are stored in:

    >> File.binread("arrow.png").unpack("xA3x8A4NN")
    => ["PNG", "IHDR", 42, 23]

With some modifications, this code could be wrapped into something like the
following:

    image = PNG.open("arrow.png")
    image.width  #=> 42
    image.height #=> 23

Your goal will be to do something similar for a file type of your own choosing.

## QUESTIONS?

Hit up the mailing list or IRC. RMU exercises are left deliberately open ended,
and often benefit from some discussion before, during, and after you work on
them. 
