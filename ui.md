ui
==

- everything is done in compositing layers and the grpahic daemon manages those and writes them to the screen daemon
- screen daemon manages screens connected and stores pixel buffers
- usually the compositing daemon will be the only thing writing to the screen daemon but it could allow for fast fullscreen gaming where the graphic daemon is told to pause and a new pixel buffer is made for the application
