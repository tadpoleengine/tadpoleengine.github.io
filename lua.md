first round of lua scripting support
===

After getting all the projects set up on all six platforms, the next task for me was to get a basic Lua proof-of-concept working. Rather than making one small thing work and then spending lots of time porting it to every platform, I decided to get a bigger PoC working, then invest in getting it to be portable.

I wanted the proof of concept to also include all third-party libraries that I planned to use for the whole project, so I wouldn't have to bother with them later. That meant not only Lua, but all the SDL supporting libraries: SDL_Image, SDL_TTF, SDL_Net, and SDL_Mixer. I anticipated it being a PITA to get these libraries up and running on every platform, and I was right.

Here's the test Lua script running on my Mac:

[![Lua scripting proof of concept](https://img.youtube.com/vi/tMigtkG_9Gk/0.jpg)](https://www.youtube.com/watch?v=tMigtkG_9Gk)

You can't hear it in the video, but it's playing Rick Astley's "Never Gonna Give You Up" in the background.

That demo was created with this code:

```
x = 0
y = 0
speed = 5
greenface = lib.load_image("assets/img/greenface.png")
font = lib.load_font("assets/fonts/free-sans.ttf", 20)

platform_text = "you are on " .. lib.get_platform()
response_text = lib.network_request("google.com", "/")
hello_world_text = lib.load_text(font, platform_text .. "\r\n" .. response_text, {r=0, g=255, b=0})

song = lib.load_music("assets/sounds/rick_astley.mp3")
lib.play_music(song, -1)

function frame ()
    lib.fill_screen_with_color(100, 100, 100)
    if lib.has_keyboard() then
        if lib.is_key_pressed("Left") then
            x = x - speed
        end
        if lib.is_key_pressed("Right") then
            x = x + speed
        end
        if lib.is_key_pressed("Up") then
            y = y - speed
        end
        if lib.is_key_pressed("Down") then
            y = y + speed
        end
    end
    touch_x, touch_y = lib.get_touch_coordinates()
    if touch_x and touch_y then
        lib.draw_texture(touch_x, touch_y, greenface)
    end
    lib.draw_texture(x, y, greenface)
    lib.draw_texture(0, 10, hello_world_text)
    lib.render()
end
```

As you can see it's pretty ugly, but it shows all the important building blocks:

* displaying an image on the screen
* detecting the user's platform
* making a network request
* displaying text
* accepting user input from the keyboard
* registering user touches from the mouse
* playing sounds

I believe that is all I need to get the rest of the platform up and running. There are plenty more integrations that I will need to make, but the libraries to do so are all already there.

I am REALLY glad I chose Lua for this project. Lua is basically just a C library. No other mainstream language that I know of was designed to be so easy to embed into other applications. I can see why it's the de facto standard of the gaming industry.

Library design will be an interesting challenge -- right now, the rostrum libraries are available to the user through the global `lib` variable. If the library gets much bigger (which I guess it probably will) then I may have to reconsider the API somewhat.

My biggest concern right now is that SDL_Net doesn't support IPv4 ... some forums online recommended just using BSD sockets but I'm nervous that iOS, Android, and Windows might not support them. Oh well, that's a problem for future me.

After getting this demo to work on Mac OS, I immediately ran into an immense amount of trouble trying to get it to work on Emscripten. Details in the next post!
