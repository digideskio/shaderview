![screenshot 2015-07-28 18 41 49](https://cloud.githubusercontent.com/assets/9792/8938008/2bacab68-355c-11e5-899a-dcd90928be12.png)

Mad scrawlings of thoughts and ideas. Work in progress. Unstable.

### OSC based Uniforms

Osc Server listening on port 9177: 

```
Messages / Arguments
* "/uniform" <UniformName> <FloatValue>
* "/smoothed-uniform" <UniformName> <FloatValue>
* "/shader" <StringValue>
```

The uniforms are updated and sent to running shader.

Ruby Example:
```ruby
require 'osc-ruby'
@client = OSC::Client.new('localhost', 9177)
@client.send(OSC::Message.new("/shader" , "/Users/josephwilk/shaders/wave.glsl"))
```

Clojure example:
```clojure
(use 'overtone.osc)
(def client (osc-client "localhost" 9177))

(osc-send client "/uniform" "iExample" (float 100.0))
(osc-send client "/shader" "/usr/josephwilk/repl_electric.glsl")
```

### OpenFramework Plugins

* https://github.com/kylemcdonald/ofxFft
* https://github.com/bakercp/ofxIO
* https://github.com/hideyukisaito/ofxOsc
* https://github.com/darrenmothersele/ofxEditor
* https://github.com/neilmendoza/ofxPostProcessing

### Build/Install instructions

#### Ubuntu

Some notes from @mattrei on the process to get an install on Ubuntu:  

* ofxEditor: would not compile because in the src/ClipBoard.cpp the ClipBoard.h is spelled wrongly. Did a pull request already there. for now we have to fix it manually.

* ofxOsc: dont use the addon which ships with oF 8.0.x; use that one which is suggested in the README.md of shaderview

* ofxPostProcessing: the current master is not working with the latest oF 8.0.4: in src/PostProcessing.h in line 52 and 53 remove the 'const' so it machte oF function signatures

* ofxFft: you need this library 'sudo apt-get install libfftw3-dev '; and then in shaderviews 'config.make' add 'USER_LDFLAGS = -lfftw3f'

### Credits

Inspired by Roger Allen's Shadertone: https://github.com/overtone/shadertone

##License

Copyright © 2015 Joseph Wilk

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

For full license information, see the LICENSE file.
