# TV on the Radio

An application that displays images from the TV every 5 or 10 seconds on a connected second screen.

Partially implemented in [this fork](https://github.com/libbymiller/radiodan/tree/libby-experiments)

* Just uses the tiny web server to load an image every 5 or 10 seconds, based on the time as fed to the server from Radiodan.

The images were created using ffmpeg from an mp4:

    #!/usr/bin/env ruby
    # pass the video source file(s) into the command line args
    # resulting images are jpg, just change the appropriate ffmpeg option for png.
    # the last line uses ImageMagick to stitch the images together into a strip.    
    # the first image is thrown away, since it's a duplicate of the second image.
    # http://stackoverflow.com/questions/3306888/ffmpeg-generate-n-evenly-spaced-png-screenshots

    ARGV.each do|a|
      total_shots = 354
      size = '768x576'
      meta = %x(ffmpeg -i #{a} 2>&1 | grep 'Duration' | cut -d ' ' -f 4 | sed s/,//)
      time_parts = meta.match /(\d\d):(\d\d):(\d\d)\.(\d\d)/
      duration_seconds = time_parts[1].to_i*60*60+time_parts[2].to_i*60+time_parts[3].to_i+time_parts[4].to_f/100
      puts "*** Duration seconds: " +  duration_seconds.to_s
      %x(ffmpeg -i #{a} -r #{total_shots/duration_seconds} -s #{size} -f image2 -vframes #{total_shots+1} img-%03d.jpg )
      files = (1..total_shots+1).map{|i| 'img-' + ("%03d" % i) + '.jpg'}
      files.delete_at 0
      # %x(convert -append #{files.join ' '} shot-strip.jpg)
    end

