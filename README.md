# Encrypted Infinite Storage Glitch
A Python3 implementation of the Infinite Storage Glitch that incorporates AES encryption

<h2>Brief Overview</h2>

<p>
  The infinite storage glitch is a method of using video streaming platforms as a means of cloud storage. 
  Essentially, the file(s) that are to be stored are converted to videos that can be uploaded to services like YouTube. 
  When the original files are required the video can be downloaded from YouTube (or any similar service) and it can be 
  decoded back into the encoded files. This is a project I worked on as part of the honors section of my Computer Systems and programming class, ECE220.
  It differs from the original project that I found on Reddit in one key way. The original version does not use any form of encryption, 
  it simply encodes the passed in data as a video. 
</p>

<h2>High Level Program Flow</h2>

<p>
  The program flows as follows: <br>
    <ol>
      <li>An image is passed in, and it is encrypted using AES encryption</li>
      <li>The encrypted data is then converted into hexadecimal, and finally binary</li>
      <li>The binary data is encoded into PNG images, with a white pixel representing 1 and a black pixel representing 0</li>
      <li>The images are combined into a video in the AVI format, which can then be uploaded to YouTube</li>
      <li>The video can then be broken up into its frames which can then be decoded back into the original image data</li>
    </ol>
PNG images and AVI videos are used because PNG and AVI do not have any compression, this ensures that the 
original data can be recovered during decoding and for decryption.
</p>

<h2>Probabalistic Nature and Future Upgrades</h2>
<p>
  Although all the file formats used do not have any compression, some of the pixel values were changed in a manner similar to what is expected
  from a compression algorithm (similarly coloured pixels near one another were given the same value, different from the original). This is why
  the closer_to_which() function was implemented. The larger the input file, the more likely it is that a pixel will have a value that is far 
  enough from it's original value, that the string cannot be decrypted to yield the correct output. Once I am able to discern why even while using 
  file types that don;t use compression I am getting an ouput that resembles it, I can incorporate the following changes: 
  <ol>
      <li>
        Use colored pixels: Since each pixel is assigned a value between 0 and 255 (I am using only 0, 127 and 255 since they are the 
        set of 3 that is furthest apart), I no longer need to convert the strings to binary for the images. Not only does this save a step, but the 
        videos will be shorter (each hexadecimal character is 4 binary bits) and can store more data in each frame. 
      </li>
      <li>
        Storing multiple files: Right now a colour value of 127 indicates that it is a filler pixel. Since only 1 color value needs to be used 
        for filler pixels, a different color value can be selected to indicate the end of 1 file's data, so that the program can automatically 
        discern between the data of multiple files. 
      </li>
      <li>
        Password protected encryption: For AES encryption and decryption, the key and nonce used for encryption must also be used for decryption. 
        If there are multiple color values available, the key and nonce can be indicated by their own color value, and no longer need to be
        stored/remembered by the user for decryption, they can be stored in the video data itself. This defeats the purpose of encryption if any bad
        actor can access them from the video, but by allowing the user to set a password that they can remember, which protects the key and nonce this
        data too can be a part of the video. 
      </li>
      <li>
        Multiple file types: As of now, the program only allows for the encryption of image files. However, the file type can be specified using 
        metadata indicated by pixel color, such that the program is able to differentiate between what file type the data is associated with so that 
        multiple file types can be encrypted and encoded in a single video. 
      </li>
    </ol>
</p>

<h2>Key Notes + References</h2>
<p>
  There are restrictions involved with uploading videos to services like YouTube that are outlined in the terms of service. More information about 
  these restrictions, as well as the original project can be found here: <br>
  https://github.com/DvorakDwarf/Infinite-Storage-Glitch
</p>


